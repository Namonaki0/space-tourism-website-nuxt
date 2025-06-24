<template>
    <div class="header-wrapper">
      <AppLogo />
      <div class="menu-line" />
      <NavBar />
    </div>
</template>
<style lang="scss" scoped>
.header-wrapper {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem 1.5rem;
    position: absolute;
    width: 100%;

    @media (min-width: 768px) {
      padding: 0;
    }

    @media (min-width: 1024px) {
      padding-top: 40px;
    }

    .menu-line {
      flex-grow: 1;
      height: 1px;
      background-color: #979797;
      opacity: 0.25;
      margin: 0;
      z-index: 2;
      margin-right: -40px;
      margin-top: -3px;

      @media (max-width: 1023px) {
        display: none;
      }
    }
}
</style>