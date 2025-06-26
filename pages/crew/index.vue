<script setup lang="ts">
import { crew } from '@/data/crew'

const memberIndex = ref(0)
const member = computed(() => crew[memberIndex.value])

function setActiveMember(index: number) {
  memberIndex.value = index
}
onMounted(() => {
  memberIndex.value = 0;
});
</script>
<template>
  <div class="crew template-padding-top">
    <h1 class="section-title"><span>02</span> Meet your crew</h1>
    <section class="crew-wrapper">
      <div class="crew-info">
        <Transition name="fade-slide" mode="out-in">
            <div :key="memberIndex" class="crew-info-data">
                <p class="role">{{ member.role }}</p>
                <p class="name">{{ member.name }}</p>
                <p class="description">{{ member.description }}</p>
            </div>
        </Transition>
        <ul class="pagination-dots">
          <li
            v-for="(_, index) in crew"
            :key="index"
            :class="{ 'active': index === memberIndex }"
          >
            <button
              class="dot-cta"
              :aria-label="`Go to crew member ${index + 1}`"
              @click="setActiveMember(index)"
            />
          </li>
        </ul>
      </div>
      <Transition name="fade-slide" mode="out-in">
        <div :key="memberIndex" class="crew-image">
            <img :src="member.image" :alt="member.name">
        </div>
      </Transition>
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
          @include text-4;
          text-transform: uppercase;
          color: #aaa;
          font-size: clamp(1.5rem, 3.5vw, 1.8rem);
          line-height: unset;
          margin-bottom: 12px;

          @media (min-width: $breakpoint-desktop) {
            margin-bottom: 0;
          }
        }
  
        .name {
          @include text-3;
          font-size: 2.5rem;
          text-transform: uppercase;
          margin: 0.5rem 0 2rem;
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

          &.active {
            background: white;
          }
          
          .dot-cta {
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
