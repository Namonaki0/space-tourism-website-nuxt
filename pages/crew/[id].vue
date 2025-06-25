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
        <div class="crew-info-data">
          <p class="role">{{ member.role }}</p>
          <p class="name">{{ member.name }}</p>
          <p class="description">{{ member.description }}</p>
        </div>
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
  @include page-padding;

  .section-title {
    @include page-header-title;

    span {
      font-weight: bold;
      opacity: 0.25;
      margin-right: 1rem;
    }
  }

  .crew-wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    gap: 2rem;

    @media (min-width: $breakpoint-tablet) {
      flex-direction: row;
      align-items: end;
      flex-direction: column;
      align-items: center;
    }

    @media (min-width: $breakpoint-desktop) {
      flex-direction: row;
      align-items: center;
      width: 1110px;
      margin-left: auto;
      margin-right: auto;
    }

    .crew-info {
      max-width: 500px;
      text-align: center;

      @media (min-width: $breakpoint-desktop) {
        text-align: left;
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
      }

      .crew-info-data {
        @media (min-width: $breakpoint-desktop) {
          height: 40%;
          display: flex;
          flex-direction: column;
          justify-content: flex-end;
        }

        .role {
          font-size: 1rem;
          text-transform: uppercase;
          color: #aaa;
          @include text-4;
          font-size: clamp(1.5rem, 3.5vw, 1.8rem);
          line-height: unset;
          margin-bottom: 12px;

          @media (min-width: $breakpoint-desktop) {
            margin-bottom: 0;
          }
        }
  
        .name {
          font-size: 2.5rem;
          text-transform: uppercase;
          margin: 0.5rem 0 2rem;
          @include text-3;
          font-size: clamp(1.9rem, 6vw, 3.1rem);
          line-height: 93.2%;

          @media (min-width: $breakpoint-desktop) {
            margin-bottom: 1.5rem;
          }
        }
  
        .description {
          @include header-description;
  
          @media (min-width: $breakpoint-desktop) {
            font-size: 18px;
            margin-bottom: 0;
            padding-bottom: 0;
          }
        }
      }

      .pagination-dots {
        display: flex;
        gap: 0.5rem;
        margin-top: 2rem;
        justify-content: center;

        @media (min-width: $breakpoint-desktop) {
          justify-content: flex-start;
          gap: 2.5rem;
          margin-top: auto;
          height: 12%;
        }

        li {
          width: 10px;
          height: 10px;
          border-radius: 50%;
          background: $mute-grey;

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
      position: relative;

      &::before {
        content: "";
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 1;
        pointer-events: none;
        background: linear-gradient(
          to top,
          rgba(0, 0, 0, 0.444) 0%,
          rgba(0, 0, 0, 0) 25%,
          rgba(0, 0, 0, 0) 10%,
          rgba(0, 0, 0, 0) 90%
        );
      }

      img {
        width: 100%;
        height: auto;
        position: relative;
        z-index: 0;

      }
    }
  }
}
</style>
