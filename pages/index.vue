<template>
  <section class="hero">
    <div class="home template-padding-top">
      <div class="home-wrapper">
        <h2>
          <span class="eyebrow">So, you want to travel to</span>
          <span class="hero-title">SPACE</span>
        </h2>
        <p class="hero-description">
          Let’s face it; if you want to go to space, you might as well genuinely go to outer space and not hover kind of on the edge of it. Well sit back, and relax because we’ll give you a truly out of this world experience!
        </p>
        <div class="bubble-link-wrapper">
          <NuxtLink to="/destination/moon" title="explore" class="bubble-link" active-class="router-link-active" exact-active-class="router-link-exact-active">Explore</NuxtLink>
        </div>
      </div>
    </div>
  </section>
</template>
<style scoped lang="scss">
.home {
  height: 100dvh;
  @include responsive-bg('home');
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  color: $blue-300;

  .home-wrapper {
    text-align: center;
    h2 {
      .eyebrow {
        @include text-5;
        font-weight: 100;
        display: block;
        text-transform: uppercase;
      }

      .hero-title {
        @include text-1;
        font-weight: 100;
        color: $white;
      }
    }

    .hero-description {
      @include text-9;
      margin-top: 0.5rem;
      margin-bottom: 5.5rem;
    }

    .bubble-link-wrapper {
      display: flex;
      justify-content: center;
      
      .bubble-link {
        position: relative;
        @include text-4;
        text-decoration: none;
        text-transform: uppercase;
        cursor: pointer;
        border-radius: 50%;
        width: 144px;
        height: 144px;
        display: grid;
        place-content: center;
        background: $white;
        color: $blue-900;
        font-size: 24px;
        transition: color 0.3s ease-in;

        &::after {
          content: '';
          position: absolute;
          top: 50%;
          left: 50%;
          width: 0px;
          height: 0px;
          border-radius: 50%;
          background: rgba(255, 255, 255, 0.114);
          transform: translate(-50%, -50%);
          opacity: 0;
          pointer-events: none;
          transition: opacity 0.3s ease-in-out, 
                      width 0.2s ease-in-out, 
                      height 0.2s ease-in-out;
        }

        &:hover::after,
        &:focus::after {
          opacity: 1;
          width: 220px;
          height: 220px;
        }
      }
    }
  }
}
</style>
