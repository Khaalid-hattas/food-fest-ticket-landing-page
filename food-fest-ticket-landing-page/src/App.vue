<template>
  <main class="container">
    <EventHeader />

    <TicketList />
  </main>
</template>

<script setup>
import EventHeader from './components/headersection.vue'; // Matches your lowercase file name
import TicketList from './components/ticketlist.vue';     // Matches your lowercase file name
</script>