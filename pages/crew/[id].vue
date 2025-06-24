<script setup lang="ts">
import { crew } from '@/data/crew'

const member = ref(crew[0])
const memberIndex = ref(0)

watch(
  () => useRoute().params.id,
  (newId) => {
    const index = parseInt(newId as string) - 1
    if (isNaN(index) || !crew[index]) {
      useRouter().replace('/crew/1')
    } else {
      memberIndex.value = index
      member.value = crew[index]
    }
  },
  { immediate: true }
)
</script>
<template>
  <div class="crew template-padding-top">
    <h1 class="section-title"><span>02</span> Meet your crew</h1>
    <section class="crew-wrapper">
      <div class="crew-info">
        <p class="role">{{ member.role }}</p>
        <h2 class="name">{{ member.name }}</h2>
        <p class="description">{{ member.description }}</p>

        <ul class="pagination-dots">
          <li
            v-for="(_, index) in crew"
            :key="index"
            :class="{ 'router-link-active': index === memberIndex }"
          >
            <NuxtLink :to="`/crew/${index + 1}`" class="dot-link" active-class="router-link-active" exact-active-class="router-link-exact-active"/>
          </li>
        </ul>
      </div>

      <div class="crew-image">
        <img :src="member.image" :alt="member.name">
      </div>
    </section>
  </div>
</template>
<style scoped lang="scss">
.crew {
  height: 100dvh;
  display: flex;
  flex-direction: column;
  @include responsive-bg('crew');

  .section-title {
    text-transform: uppercase;
    font-size: 1rem;
    letter-spacing: 2px;
    margin-bottom: 2rem;

    span {
      font-weight: bold;
      opacity: 0.25;
      margin-right: 1rem;
    }
  }

  .crew-wrapper {
    display: flex;
    flex-direction: column-reverse;
    align-items: center;
    justify-content: space-between;
    gap: 2rem;

    @media (min-width: 768px) {
      flex-direction: row;
      align-items: end;
    }

    .crew-info {
      max-width: 500px;
      text-align: center;

      @media (min-width: 768px) {
        text-align: left;
      }

      .role {
        font-size: 1rem;
        text-transform: uppercase;
        color: #aaa;
      }

      .name {
        font-size: 2.5rem;
        text-transform: uppercase;
        margin: 0.5rem 0;
      }

      .description {
        font-size: 1rem;
        line-height: 1.6;
        color: #ccc;
      }

      .pagination-dots {
        display: flex;
        gap: 0.5rem;
        margin-top: 2rem;
        justify-content: center;

        li {
          width: 10px;
          height: 10px;
          border-radius: 50%;
          background: white;

          &.router-link-active {
            background: white;
          }
          
          .dot-link {
            cursor: pointer;
            display: block;
            border-radius: 50%;
            width: 100%;
            height: 100%;
          }
        }
      }
    }

    .crew-image {
      img {
        height: auto;
        max-height: 400px;
        object-fit: contain;
      }
    }
  }
}
</style>
