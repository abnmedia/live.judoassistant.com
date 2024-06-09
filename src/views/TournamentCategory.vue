<template>
  <InfoText v-if="categoryState == 'NOT_LOADED'" icon="cloud-off-outline">Category not found. The category does not exist.</InfoText>
  <InfoText v-if="categoryState == 'LOADING'" icon="loading" rotating>Loading category..</InfoText>
  <template v-if="categoryState == 'LOADED'">
    <h2>{{ category.name }}</h2>
    <Tabs>
      <TabItem title="Players" selected="true">
        <InfoText v-if="players.length == 0">This category has no players.</InfoText>
        <Table v-if="players.length > 0" :headers="playerTableHeaders" :rows="players" v-slot="props">
          <TableColumn>
            <router-link class="menu-item" :to="{ name: 'tournament-player', params: { tournament: this.$route.params.tournament, playerId: props.row.id }}">{{ props.row.firstName }}</router-link>
          </TableColumn>
          <TableColumn>
            {{ props.row.lastName }}
          </TableColumn>
          <TableColumn>
            {{ props.row.club }}
          </TableColumn>
        </Table>
      </TabItem>

      
    </Tabs>
  </template>
</template>

<script>
/* <TabItem :label="'Tatami ' + (index + 1)" :key="index" v-for="(matches, index) of tatamiMatches"> */
import { mapState, mapGetters } from 'vuex'
import Tabs from '@/components/Tabs.vue'
import TabItem from '@/components/TabItem.vue'
import Table from '@/components/Table.vue'
import TableColumn from '@/components/TableColumn.vue'
import InfoText from '@/components/InfoText.vue'

export default {
  components: { Tabs, TabItem, Table, TableColumn, InfoText },
  data() {
    return {
      playerTableHeaders: [
        { 'field': 'firstName', 'label': 'First Name', 'sortable': true },
        { 'field': 'lastName', 'label': 'Last Name', 'sortable': true },
        { 'field': 'club', 'label': 'Club', 'sortable': true },
      ],
    }
  },
  mounted: function() {
    this.$store.dispatch('subscribeCategory', this.$route.params.categoryId);
  },
  watch: {
    '$route.params.categoryId': function() {
      this.$store.dispatch('subscribeCategory', this.$route.params.categoryId);
    }
  },
  computed: {
    ...mapState({
      categoryState: state => state.categoryState,
      category: state => state.category,
    }),
    ...mapGetters({
      players: 'categoryPlayers',
    }),
  },
}
</script>

