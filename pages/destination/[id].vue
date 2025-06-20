<script setup lang="ts">
import { destinations } from '@/data/destinations'

const route = useRoute()
const router = useRouter()

const planetParam = route.params.id
const data = destinations[planetParam as keyof typeof destinations]

if (!data) {
  router.push('/destination/moon')
}
</script>

<template>
  <div class="destination-page">
    <h1><span>01</span> PICK YOUR DESTINATION</h1>

    <div class="image">
      <img :src="data.image" :alt="data.name" />
    </div>

    <nav class="tabs">
      <NuxtLink
        v-for="(val, key) in destinations"
        :key="key"
        :to="`/destination/${key}`"
        :class="{ active: key === planetParam }"
      >
        {{ key.toUpperCase() }}
      </NuxtLink>
    </nav>

    <div class="content">
      <h2>{{ data.name }}</h2>
      <p>{{ data.description }}</p>

      <div class="meta">
        <div>
          <h3>AVG. DISTANCE</h3>
          <p>{{ data.distance }}</p>
        </div>
        <div>
          <h3>EST. TRAVEL TIME</h3>
          <p>{{ data.travelTime }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
