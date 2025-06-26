<script setup lang="ts">
import { technology } from "@/data/technology";

const technologyIndex = ref(0);
const selectedTechnology = computed(() => technology[technologyIndex.value]);

function selectTechnology(index: number) {
  technologyIndex.value = index;
}

onMounted(() => {
  technologyIndex.value = 0;
});
</script>

<template>
  <div class="technology template-padding-top">
    <h1 class="container-title"><span>03</span> space launch 101</h1>
    <div class="container-inner">
      <Transition name="fade-slide" mode="out-in">
        <div :key="technologyIndex" class="technology-image">
          <picture>
            <source :srcset="selectedTechnology.images.portrait" media="(min-width: 1024px)" />
            <source
              :srcset="selectedTechnology.images.landscape"
              media="(min-width: 760px) and (max-width: 1023px)"
            />
            <img :src="selectedTechnology.images.portrait" :alt="selectedTechnology.name" />
          </picture>
        </div>
      </Transition>
      <div class="pagination-wrapper">
        <ul class="pagination-bubbles">
          <li
            v-for="(_, index) in technology"
            :key="index"
            :class="{ active: index === technologyIndex }"
          >
            <button
              :class="{ active: index === technologyIndex }"
              class="bubble-cta"
              @click="selectTechnology(index)"
            >
              {{ index }}
            </button>
          </li>
        </ul>
        <Transition name="fade-slide" mode="out-in">
          <section :key="technologyIndex" class="technology-data">
            <p class="role">the terminology...</p>
            <p class="name">{{ selectedTechnology.name }}</p>
            <p class="description">{{ selectedTechnology.description }}</p>
          </section>
        </Transition>
      </div>
    </div>
  </div>
</template>
<style lang="scss">
@import "@/assets/styles/variables.scss";
.technology {
  @include responsive-bg("technology");
  min-height: 100vh;
  overflow-x: hidden;

  .container-title {
    @include page-header-title;
    margin-bottom: 88px;

    span {
      font-weight: bold;
      opacity: 0.25;
      margin-right: 1rem;
    }
  }

  .container-inner {
    min-height: 515px;

    @media (min-width: $breakpoint-tablet) {
      min-height: 763px;
    }

    @media (min-width: $breakpoint-desktop) {
        display: flex;
        flex-direction: row-reverse;
        width: 1275px;
        margin-left: auto;
        min-height: 515px;
    }

    .technology-image {
      @media (min-width: $breakpoint-desktop) {
        margin-bottom: 115px;
      }

      img {
        margin: 0 auto;
      }
    }

    .pagination-wrapper {
      min-height: 200px;
      position: relative;
      @media (min-width: $breakpoint-desktop) {
        display: flex;
      }

      .pagination-bubbles {
        display: flex;
        gap: 0.5rem;
        margin-top: 2rem;
        justify-content: center;
        @include page-padding;
        gap: 1rem;
        margin-bottom: 40px;

        @media (min-width: $breakpoint-desktop) {
          flex-direction: column;
          margin-bottom: 150px;
          margin-top: 0;
          padding-right: 32px;
        }

        li {
          width: 40px;
          height: 40px;
          border-radius: 50%;
          background: transparent;
          display: grid;
          place-content: center;

          @media (min-width: $breakpoint-tablet) {
            width: 56px;
            height: 56px;
          }

          @media (min-width: $breakpoint-desktop) {
            width: 80px;
            height: 80px;
          }

          .bubble-cta {
            @include text-4;
            cursor: pointer;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            text-decoration: none;
            display: grid;
            place-content: center;
            cursor: pointer;
            border: 1px solid $white;
            color: $white;
            transition: all 0.2s ease-in-out;
            font-size: 20px;
            font-weight: 100;

            @media (min-width: $breakpoint-tablet) {
              width: 56px;
              height: 56px;
            }

            @media (min-width: $breakpoint-desktop) {
              width: 80px;
              height: 80px;
              font-size: 24px;
            }

            &:hover,
            &:focus {
              background: $white;
              color: $blue-900;
            }

            &.active {
              background: $white;
              color: $blue-900;
            }
          }
        }
      }

      .technology-data {
        @include page-padding;
        text-align: center;

        @media (min-width: $breakpoint-desktop) {
          text-align: left;
          display: flex;
          flex-direction: column;
          justify-content: center;
          align-items: flex-start;
          padding-left: 32px;
          margin-bottom: 115px;
        }

        .role {
          @include text-4;
          text-transform: uppercase;
          color: #aaa;
          font-size: clamp(1.5rem, 3.5vw, 1.8rem);
          margin-bottom: 16px;
          line-height: unset;
        }

        .name {
          @include text-3;
          font-size: 2.5rem;
          text-transform: uppercase;
          margin: 0.5rem 0 2rem;
          font-size: clamp(1.9rem, 6vw, 3.1rem);
        }

        .description {
          @include header-description;
          padding-bottom: 48px;
          margin-bottom: 0;

          @media (min-width: $breakpoint-tablet) {
            font-size: 19px;
            width: 512px;
            margin: 0 auto;
            padding-bottom: 40px;
          }

          @media (min-width: $breakpoint-desktop) {
            font-size: 21px;
          }
        }
      }
    }
  }
}

.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: opacity 0.3s, transform 0.2s;
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
