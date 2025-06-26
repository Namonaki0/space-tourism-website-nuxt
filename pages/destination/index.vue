<script setup lang="ts">
import { destinations } from '@/data/destinations'

const destinationIndex = ref(0)
const selectedDestination = computed(() => destinations[destinationIndex.value])

function selectDestination(index: number) {
  destinationIndex.value = index
}

onMounted(() => {
  destinationIndex.value = 0
})
</script>
<template>
  <div class="destination template-padding-top">
    <h1 class="section-title"><span>01</span> PICK YOUR DESTINATION</h1>
    <div class="destination-inner">
      <Transition name="fade-slide" mode="out-in">
        <AppImage 
        :key="destinationIndex"
        :data="selectedDestination" 
        />
      </Transition>
      <div class="destination-inner-data">
        <nav :key="destinationIndex" class="tabs">
          <button
            v-for="(dest, index) in destinations"
            :key="dest.id"
            :class="{ active: index === destinationIndex }"
            class="crew-info-data"
            @click="selectDestination(index)"
          >
            {{ dest.name.toUpperCase() }}
          </button>
        </nav>
        <Transition name="fade-slide" mode="out-in">
          <div :key="destinationIndex" class="destination-content">
            <p class="name">{{ selectedDestination.name }}</p>
            <p class="description">{{ selectedDestination.description }}</p>

            <div class="meta">
              <div>
                <h3>AVG. DISTANCE</h3>
                <p>{{ selectedDestination.distance }}</p>
              </div>
              <div>
                <h3>EST. TRAVEL TIME</h3>
                <p>{{ selectedDestination.travelTime }}</p>
              </div>
            </div>
          </div>
        </Transition>
      </div>
    </div>
  </div>
</template>
<style scoped lang="scss">
.destination {
  min-height: 100dvh;
  @include responsive-bg('destination');
  @include page-padding;
  text-align: center;

  @media (min-width: $breakpoint-tablet) {
    padding-bottom: 40px;
  }

  @media (min-width: $breakpoint-desktop) {
    padding-bottom: 0;
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

  .section-title {
    @include page-header-title;

    span {
      color: $mute-grey;
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

    button {
      padding-bottom: 15px;
      border-bottom: 3px solid transparent;
      text-decoration: none;
      transition: all 0.3s ease-in-out;
      color: $blue-300;
      letter-spacing: 1px;
      padding: 0 0 10px;

      &:hover,
      &.focus {
        border-bottom: 3px solid $white;
        color: $white;
      }

      &.active {
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
      @include header-description;
      border-bottom: 1px solid $separator;

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
        padding-bottom: 24px;
        line-height: unset;
      }
    }
  }
}

.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: opacity 0.4s, transform 0.4s;
}
.fade-slide-enter-from,
.fade-slide-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
.fade-slide-enter-to,
.fade-slide-leave-from {
  opacity: 1;
  transform: translateX(0);
}
</style>