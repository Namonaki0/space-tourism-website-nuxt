<script setup lang="ts">
import { technology } from '@/data/technology'

const tech = ref(technology[0])
const techIndex = ref(0)

watch(
  () => useRoute().params.id,
  (newId) => {
    const index = parseInt(newId as string) - 1
    if (isNaN(index) || !technology[index]) {
      useRouter().replace('/technology/1')
    } else {
      techIndex.value = index
      tech.value = technology[index]
    }
  },
  { immediate: true }
)
</script>

<template>
  <div class="technology template-padding-top">
    <h1 class="container-title"><span>03</span> space launch 101</h1>
    <div class="container-inner">
      <div class="technology-image">
        <picture>
          <source
            :srcset="tech.images.portrait"
            media="(min-width: 1024px)"
          >
          <source
            :srcset="tech.images.landscape"
            media="(min-width: 760px) and (max-width: 1023px)"
          >
          <img
            :src="tech.images.portrait"
            :alt="tech.name"
          >
        </picture>
      </div>
      <div class="pagination-wrapper">
        <ul class="pagination-bubbles">
          <li
            v-for="(_, index) in technology"
            :key="index"
            :class="{ 'router-link-active': index === techIndex }"
          >
            <NuxtLink :to="`/technology/${index + 1}`" class="bubble-link" active-class="router-link-active" exact-active-class="router-link-exact-active">
              <span>{{ index + 1 }}</span>
            </NuxtLink>
          </li>
        </ul>
        <section class="technology-data">
          <p class="role">the terminology...</p>
          <p class="name">{{ tech.name }}</p>
          <p class="description">{{ tech.description }}</p>
        </section>
      </div>
    </div>
  </div>
</template>
<style lang="scss">
@import '@/assets/styles/variables.scss';
.technology {
  min-height: 100vh;
  @include responsive-bg('technology');

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

    @media (min-width: $breakpoint-desktop) {
      display: flex;
      flex-direction: row-reverse;
      width: 1275px;
      margin-left: auto;
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
            
            .bubble-link {
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
  
                @media (min-width: $breakpoint-tablet) {
                  width: 56px;
                  height: 56px;
                }
  
                @media (min-width: $breakpoint-desktop) {
                  width: 80px;
                  height: 80px;
                }
  
                &:hover,
                &:focus {
                  background: $white;
                  color: $blue-900;
                }
  
                &.router-link-active,
                &.router-link-exact-active {
                  background: $white;
                  color: $blue-900;
  
                  span {
                    @include text-4;
                    font-size: 20px;
                    font-weight: 100;
  
                    @media (min-width: $breakpoint-desktop) {
                      font-size: 28px;
                    }
                  }
                }   
                
                span {
                  @media (min-width: $breakpoint-desktop) {
                    font-size: 28px;
                    font-family: 'Bellefair', serif;
                  }
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
          line-height: unset
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
</style>
