<template>
  <h2>Overview</h2>
  <table>
    <tr>
      <th>Tournament</th>
      <td>{{ tournament.name }}</td>
    </tr>
    <tr>
      <th>Date</th>
      <td>{{ dateFilter(tournament.date) }}</td>
    </tr>
    <tr>
      <th>Location</th>
      <td>{{ tournament.location }}</td>
    </tr>
  </table>

</template>

<script>
/* <TabItem :label="'Tatami ' + (index + 1)" :key="index" v-for="(matches, index) of tatamiMatches"> */
import { mapId } from '@/store/helpers.js'
import { dateFilter } from '@/store/filters.js'
import { mapState, mapGetters } from 'vuex'

export default {
  mounted: function() {
    /* this.$store.dispatch('subscribeTournament', this.$route.params.tournament); */
  },
  computed: {
    ...mapState({
      tournamentState: state => state.tournamentState,
      tournament: state => state.tournament,
    }),
  },
  methods: {
    mapId: mapId,
    dateFilter: dateFilter,
  }
}
</script>

