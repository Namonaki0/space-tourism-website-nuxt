<template>
    <div class="logo-wrapper">
        <NuxtLink to="/" class="logo-link">
            <img 
                src="~/assets/images/shared/logo.svg"
                width="100"
                height="100"
                alt="Space Tourism Logo"
                class="logo"
            >
        </NuxtLink>
    </div>
</template>
<style scoped lang="scss">
.logo-wrapper {
    @media (min-width: $breakpoint-tablet) {
        width: clamp(50px, 18vw, 170px);
        padding: 0.5rem 2.5rem;
        z-index: 2;
    }

     @media (min-width: $breakpoint-desktop) {
        padding: 1rem 3.5rem;
    }

    .logo {
       width: 100%;
       height: auto;
    }
}
</style>