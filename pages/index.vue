<template>
  <section class="hero">
    <div class="home template-padding-top">
      <h1><span>01.</span> pick your destination</h1>
      <div class="home-wrapper">
        <h2>
          <span class="eyebrow">So, you want to travel to</span>
          <span class="hero-title">SPACE</span>
        </h2>
        <p class="hero-description">
          Let’s face it; if you want to go to space, you might as well genuinely go to outer space and not hover kind of on the edge of it. Well sit back, and relax because we’ll give you a truly out of this world experience!
        </p>
        <NuxtLink to="/destination/moon" title="explore" class="hero-cta" active-class="router-link-active" exact-active-class="router-link-exact-active">Explore</NuxtLink>
      </div>
    </div>
  </section>
</template>
<style scoped lang="scss">
.home {
  height: 100dvh;
  @include responsive-bg('home');
}
</style>
