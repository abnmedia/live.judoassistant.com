<template>
  <main>
    <InfoText v-if="tournamentState == 'NOT_LOADED'" icon="cloud-off-outline">Tournament not found. The tournament does not exist.</InfoText>
    <InfoText v-if="tournamentState == 'LOADING'" icon="loading" rotating>Loading tournament..</InfoText>
    <template v-if="tournamentState == 'LOADED'">
      <h1>{{ tournament.name }}</h1>
      <router-view></router-view>
    </template>
  </main>
</template>