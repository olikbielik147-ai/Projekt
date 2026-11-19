<script setup>
import dataDestinations from '../data.json'
const destinations = dataDestinations.destinations
</script>

<template>
  <nav id="nav">
    <router-link to="/">Home</router-link>
    <router-link
      v-for="destination in destinations"
      :key="destination.id"
      :to="{ name: 'destination', params: { slug: destination.slug } }"
    >
      {{ destination.name }}
    </router-link>
  </nav>
</template>

