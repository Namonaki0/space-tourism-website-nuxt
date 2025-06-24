<script setup lang="ts">
const menuOpen = ref(false);
const isMobile = ref(false);

function handleResize() {
  isMobile.value = window.innerWidth < 768
}

function handleClickOutside(event: MouseEvent) {
  if (
    menuOpen.value &&
    isMobile.value &&
    !(event.target as HTMLElement).closest('.navbar-wrapper') &&
    !(event.target as HTMLElement).closest('.open-menu')
  ) {
    menuOpen.value = false
  }
}

onMounted(() => {
    handleResize()
  window.addEventListener('resize', handleResize)
  document.addEventListener('mousedown', handleClickOutside)
})
onUnmounted(() => {
  window.removeEventListener('resize', handleResize)
  document.addEventListener('mousedown', handleClickOutside)
})

const router = useRouter()
watch(
  () => router.currentRoute.value.fullPath,
  () => {
    if (isMobile.value) {
        setTimeout(() => {
            menuOpen.value = false
        }, 200)
    }
  }
)
</script>
<template>
    <img v-if="!menuOpen" class="open-menu" src="~/assets/images/shared/icon-hamburger.svg" alt="open menu icon" @click="menuOpen = true">
    <Transition v-if="isMobile" name="slide">
        <div v-if="menuOpen" class="navbar-wrapper">
            <img class="close-menu" src="~/assets/images/shared/icon-close.svg" alt="close menu icon" @click="menuOpen = false">
            <NuxtLink to="/" title="Home" active-class="active" :exact="false"><span>00 </span>Home</NuxtLink>
            <NuxtLink to="/destination/moon" title="Destination" active-class="active" :exact="false"><span>01 </span>Destination</NuxtLink>
            <NuxtLink to="/crew/1" title="Crew" active-class="active" :exact="false"><span>02 </span>Crew</NuxtLink>
            <NuxtLink to="/technology/1" title="Technology" active-class="active" :exact="false"><span>03 </span>Technology</NuxtLink>
        </div>
    </Transition>
    <div v-else class="navbar-wrapper">
    <img class="close-menu" src="~/assets/images/shared/icon-close.svg" alt="close menu icon" @click="menuOpen = false">
        <NuxtLink to="/" title="Home" active-class="active" :exact="false"><span>00 </span>Home</NuxtLink>
        <NuxtLink to="/destination/moon" title="Destination" active-class="active" :exact="false"><span>01 </span>Destination</NuxtLink>
        <NuxtLink to="/crew/1" title="Crew" active-class="active" :exact="false"><span>02 </span>Crew</NuxtLink>
        <NuxtLink to="/technology/1" title="Technology" active-class="active" :exact="false"><span>03 </span>Technology</NuxtLink>
    </div>
</template>
<style scoped lang="scss">
.open-menu {
    cursor: pointer;

    @media (min-width: 768px) {
        &.open-menu {
            display: none;
        }
    }
}
.navbar-wrapper {
    height: 100dvh;
    width: 65%;
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    display: flex;
    flex-direction: column;
    padding: 33% 0 20% 8%;
    background: rgba(255, 255, 255, 0.04);
    backdrop-filter: blur(30px);
    -webkit-backdrop-filter: blur(30px);

    @media (min-width: $breakpoint-tablet) {
        position: relative;
        height: auto;
        flex-direction: row;
        width: 100%;
        justify-content: space-around;
        padding: 0;
    }

    @media (min-width: $breakpoint-desktop) {
        width: max-content;
        gap: 48px;
    }

    img {
        position: absolute;
        top: 3%;
        right: 10%;
        width: 7%;
    }

    span {
        font-weight: 700;
        margin-right: 6px;
    }

    a {
        color: $white;
        font-size: 1.2rem;
        text-transform: uppercase;
        margin-bottom: 1.5rem;
        letter-spacing: 2px;
        text-decoration: none;
        font-weight: 100;
        transition: all 0.3s ease-in-out;

        &:hover {
            border-right: 5px solid $white;

            @media (min-width: $breakpoint-tablet) {
                border-right: none;
                border-bottom: 5px solid $white;
            }
        }

        @media (min-width: $breakpoint-tablet) {
            margin-bottom: 0;
            padding: 2.8rem 0;
            border-bottom: 5px solid transparent;
        }

        @media (min-width: $breakpoint-desktop) {
            &:first-of-type {
                margin-left: 159px;
            }
            &:last-of-type {
                margin-right: 64px;
            }
        }

        .active {
            border-right: 5px solid $selected;

            @media (min-width: $breakpoint-tablet) {
                border-right: none;
                border-bottom: 5px solid $selected;
            }
        }
    }

    .close-menu {
        cursor: pointer;
        width: 1.5rem;

        @media (min-width: $breakpoint-tablet) {
            display: none;
        }
    }

    .router-link-active,
    .router-link-exact-active {
        border-right: 5px solid $selected;

        @media (min-width: $breakpoint-tablet) {
            border-right: none;
            border-bottom: 5px solid $selected;
        }
    }
}

.slide-enter-from,
.slide-leave-to {
    transform: translateX(100%);
}
.slide-enter-active,
.slide-leave-active {
    transition: all 0.2s ease-in-out;
}
.slide-enter-to,
.slide-leave-from {
    transform: translateX(0);
}
</style>