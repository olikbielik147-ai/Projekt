<script setup>
import { computed } from 'vue'
import dataDestinations from '../data.json'
import experienceCard from '../components/ExperienceCard.vue'

const props = defineProps({
  slug: {
    type: String,
    required: true
  }
})

const destination = computed(() => {
  return dataDestinations.destinations.find(
    (destination) => destination.slug === props.slug
  )
})
</script>

<template>
  <section v-if="destination" class="destination">
    <h1>{{ destination.name }}</h1>
    <button @click="$router.back()">GO BACK</button>
    <div class="destination-details">
      <img :src="'/images/' + destination.image" :alt="destination.name" />
      <p>{{ destination.description }}</p>
    </div>
  </section>

  <section v-if="destination" class="experiences">
    <h2>Top Experiences in {{ destination.name }}</h2>
    <div class="cards">
      <router-link
        v-for="experience in destination.experiences"
        :key="experience.slug"
        :to="{ name: 'experience', params: { experienceSlug: experience.slug } }"
      >
        <experienceCard :experience="experience" />
      </router-link>
    </div>
    <router-view />
  </section>
</template>