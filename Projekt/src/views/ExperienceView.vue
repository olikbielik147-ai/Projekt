<script setup>
import { computed } from 'vue'
import dataDestinations from '../data.json'

const destinations = dataDestinations.destinations

const props = defineProps({
  slug: {
    type: String,
    required: true
  },
  experienceSlug: {
    type: String,
    required: true
  }
})

const destination = computed(() => {
  return destinations.find((destination) => destination.slug === props.slug)
})

const experience = computed(() => {
  return destination.value.experiences.find(
    (experience) => experience.slug === props.experienceSlug
  )
})
</script>

<template>
  <section v-if="experience" class="experience-details">
    <h2>{{ experience.name }}</h2>
    <img :src="'/images/' + experience.image" :alt="experience.name" />
    <p>{{ experience.description }}</p>
  </section>
</template>


