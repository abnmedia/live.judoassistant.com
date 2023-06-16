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