<script setup lang="ts">
const props = defineProps<{
  data: {
    image: string,
    name: string
  };
}>();

definePageMeta({
  pageTransition: {
    name: 'slide-right',
    mode: 'out-in'
  },
  middleware (to, from) {
    if (to.meta.pageTransition && typeof to.meta.pageTransition !== 'boolean')
      to.meta.pageTransition.name = +to.params.id! > +from.params.id! ? 'slide-left' : 'slide-right'
  }
})
</script>
<template>
    <div class="image">
        <img :src="props.data.image" :alt="props.data.name">
    </div>
</template>
<style scoped lang="scss">
.image {
  width: 150px;
  height: 150px;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 58.5px;

  @media (min-width: $breakpoint-tablet) {
    width: 300px;
    height: 300px;
  }

  @media (min-width: $breakpoint-desktop) {
    width: 480px;
    height: 480px;
    margin-right: 108.5px;
  }
}
.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  transition: all 0.2s;
}
.slide-left-enter-from {
  opacity: 0;
  transform: translate(50px, 0);
}
.slide-left-leave-to {
  opacity: 0;
  transform: translate(-50px, 0);
}
.slide-right-enter-from {
  opacity: 0;
  transform: translate(-50px, 0);
}
.slide-right-leave-to {
  opacity: 0;
  transform: translate(50px, 0);
}
</style>