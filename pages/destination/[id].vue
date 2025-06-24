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
  <div class="destination template-padding-top">
    <h1><span>01</span> PICK YOUR DESTINATION</h1>
    <div class="destination-inner">
      <AppImage :data="data" />
      <div class="destination-inner-data">
        <nav class="tabs">
          <NuxtLink
            v-for="(val, key) in destinations"
            :key="key"
            :to="`/destination/${key}`"
            :class="{ active: key === planetParam }"
            active-class="router-link-active"
            exact-active-class="router-link-exact-active"
          >
            {{ key.toUpperCase() }}
          </NuxtLink>
        </nav>

        <div class="destination-content">
          <p class="name">{{ data.name }}</p>
          <p class="description">{{ data.description }}</p>

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
    </div>
  </div>
</template>
<style scoped lang="scss">
.destination {
  min-height: 100dvh;
  @include responsive-bg('destination');
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  text-align: center;

  @media (min-width: $breakpoint-tablet) {
    padding-bottom: 40px;
  }

  .destination-inner {
    .destination-inner-data {
   
      @media (min-width: $breakpoint-desktop) {
        text-align: left;
      }
    }

    @media (min-width: $breakpoint-desktop) {
      display: flex;
      width: 1110px;
      margin-left: auto;
      margin-right: auto;
    }
  }

  h1 {
    font-size: 20px;
    font-weight: 100;
    letter-spacing: 1px;
    margin-bottom: 50.5px;

    @media (min-width: $breakpoint-tablet) {
      text-align: left;
      margin-left: 1rem;
    }

    @media (min-width: $breakpoint-desktop) {
      width: 1110px;
      margin-left: auto;
      margin-right: auto;
    }

    span {
      color: $span;
      font-weight: 600;
      margin-right: 24px;
    }
  }

  .tabs {
    display: flex;
    justify-content: space-evenly;
    margin-bottom: 24px;

    @media (min-width: $breakpoint-tablet) {
      width: 514px;
      margin-left: auto;
      margin-right: auto;
      justify-content: center;
      gap: 2.5rem;
    }

    @media (min-width: $breakpoint-desktop) {
      justify-content: flex-start;
    }

    a {
      padding-bottom: 15px;
      border-bottom: 3px solid transparent;
      color: $white;
      text-decoration: none;
      transition: all 0.3s ease-in-out;
      color: $blue-300;

      &:hover,
      &.focus {
        border-bottom: 3px solid $white;
        color: $white;
      }

      &.router-link-active {
        border-bottom: 3px solid $selected;
        color: $white;
      }
    }
  }

  .destination-content {
    @media (min-width: $breakpoint-tablet) {
      width: 514px;
      margin-left: auto;
      margin-right: auto;
    }

    @media (min-width: $breakpoint-desktop) {
      width: 445px;
      margin-left: 0;
      margin-right: 0;
    }

    .name {
      @include text-2;
      font-size: 56px;
      text-transform: uppercase;

      @media (min-width: $breakpoint-tablet) {
        font-size: 80px;
      }

      @media (min-width: $breakpoint-desktop) {
        font-size: 95px;
        margin-left: -8px;
      }
    }
    
    .description {
      font-size: 17px;
      color: $blue-300;
      letter-spacing: 1px;
      padding-bottom: 24px;
      border-bottom: 1px solid $separator;
      margin-bottom: 24px;
      font-weight: 100;

      @media (min-width: $breakpoint-desktop) {
        font-size: 20px;
      }
    }

    .meta {
      @media (min-width: $breakpoint-tablet) {
        display: flex;
        justify-content: space-around;
      }

      @media (min-width: $breakpoint-desktop) {
        justify-content: flex-start;
        gap: 5rem;
      }

      h3 {
        font-size: 17px;
        color: $blue-300;
        letter-spacing: 1px;
        font-weight: 100;
        margin-bottom: 10px;
      }

      p {
        @include text-6;
        margin-bottom: 24px;
        line-height: unset;
      }
    }
  }
}
</style>