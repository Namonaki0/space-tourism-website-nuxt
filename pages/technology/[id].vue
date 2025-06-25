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
    <h1 class="section-title"><span>03</span> space launch 101</h1>

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
    <section class="technology-wrapper">
      <div class="technology-info">
        <div class="technology-image">
          <picture>
            <source
              :srcset="tech.images.portrait"
              media="(max-width: 1023px)"
            >
            <img
              :src="tech.images.landscape"
              :alt="tech.name"
            >
          </picture>
        </div>
        <h2>
          <span class="role">the terminology</span>
          <span class="description">{{ tech.name }}</span>
        </h2>
      </div>
    </section>
  </div>
</template>
<style lang="scss">
@import '@/assets/styles/variables.scss';
.technology {
  height: 100dvh;
  @include responsive-bg('technology');

  .section-title {
    @include page-header-title;

    span {
      font-weight: bold;
      opacity: 0.25;
      margin-right: 1rem;
    }
  }

  .pagination-bubbles {
        display: flex;
        gap: 0.5rem;
        margin-top: 2rem;
        justify-content: center;

        li {
          width: 100px;
          height: 100px;
          border-radius: 50%;
          background: $white;
          display: grid;
          place-content: center;

          &.router-link-active,
          &.router-link-exact-active {
            background: $white;
          }
          
          .bubble-link {
            cursor: pointer;
            border-radius: 50%;
            width: 100px;
            height: 100px;
            text-decoration: none;
            display: grid;
            place-content: center;
            cursor: pointer;

            span {
              @include text-4;
              color: $blue-900;
            }
          }
        }
  }
}
</style>
