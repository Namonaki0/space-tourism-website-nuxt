<template>
  <section class="hero">
    <div class="home template-padding-top">
      <div class="home-wrapper">
        <div class="home-inner">
          <h2>
            <span class="eyebrow">So, you want to travel to</span>
            <span class="hero-title">SPACE</span>
          </h2>
          <p class="hero-description">
            Let’s face it; if you want to go to space, you might as well genuinely go to outer space and not hover kind of on the edge of it. Well sit back, and relax because we’ll give you a truly out of this world experience!
          </p>
        </div>
        <div class="bubble-link-wrapper">
          <NuxtLink to="/destination" title="explore" class="bubble-link" active-class="router-link-active" exact-active-class="router-link-exact-active">Explore</NuxtLink>
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

  .home-wrapper {
    text-align: center;

    .home-inner {
      @media (min-width: $breakpoint-desktop) {
        width: 540px;
      }

      h2 {
        .eyebrow {
          @include text-5;
          font-weight: 100;
          display: block;
          text-transform: uppercase;
          color: $blue-300;

          @media (min-width: $breakpoint-tablet) {
            font-size: 20px;
          }

          @media (min-width: $breakpoint-desktop) {
            margin-bottom: .6rem;
          }
        }

        .hero-title {
          @include text-1;
          font-weight: 100;
          color: $white;
          margin-left: -8px;

          @media (min-width: $breakpoint-tablet) {
            font-size: 108px;
          }
        }
    }

    .hero-description {
      @include header-description;
      // @include text-9;
      margin-top: 0.5rem;
      margin: 0 auto 119px;

      @media (min-width: $breakpoint-tablet) {
        width: 512px;
        font-size: 15px;
        margin-bottom: 66px;
      }

      @media (min-width: $breakpoint-desktop) {
        margin: 0;
        font-size: 19px;
      }
    }
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
        width: 132px;
        height: 132px;
        display: grid;
        place-content: center;
        background: $white;
        color: $blue-900;
        font-size: 20px;
        transition: color 0.3s ease-in;

        @media (min-width: $breakpoint-tablet) {
          width: 272px;
          height: 272px;
        }

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
          transition: opacity 0.1s ease-in-out, 
                      width 0.2s ease-in-out, 
                      height 0.2s ease-in-out;
        }

        &:hover::after,
        &:focus::after {
          opacity: 1;
          width: 240px;
          height: 240px;

            @media (min-width: $breakpoint-tablet) {
              width: 380px;
              height: 380px;
            }
        }
      }

      @media (min-width: $breakpoint-desktop) {
        margin-left: auto;
        margin-bottom: 35.5px;
      }
    }

    @media (min-width: $breakpoint-desktop) {
      display: flex;
      padding: 0 165px;
      text-align: left;
      height: 100%;
      align-items: flex-end;
      padding-bottom: 128px;
    }
  }
}
</style>
