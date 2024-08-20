<script setup>
import ArticleCard from "./components/ArticleCard.vue";
import {ref} from "vue";

const hideHeader = ref(false);

function scrollHandler(details) {
  console.log(detailsToString(details));
  if (details.inflectionPoint.top === 0) {
    hideHeader.value = false;
    return;
  }

  if (Math.abs(details.delta.top) > 40) {
    hideHeader.value = details.direction === 'down';
  }
}

function detailsToString(details) {
  return `delta: ${details.delta.top}, direction ${details.direction}, directionChanged: ${details.directionChanged}, inflectionPoint: ${details.inflectionPoint.top}, position: ${details.position.top}`;
}
</script>

<template>
  <q-layout view="hHh lpR fFf">
        <div class="n-search-layout">
          <div class="n-search-layout__header">
            <header v-show="!hideHeader"
                    :class="hideHeader ? 'animate__fadeOut' : 'animate__fadeIn'"
                    class="bg-orange-4 animate__animated">
              <div class=" q-px-md q-py-sm row q-gutter-sm">
                <q-badge color="purple" v-for="n in 28">Lorem ipsum dolor.</q-badge>
              </div>
            </header>
            <header class="bg-pink-4">
              <div class=" q-px-md q-py-sm row q-gutter-sm">
                <q-badge v-for="n in 30">Lorem ipsum.</q-badge>
              </div>
            </header>
          </div>

          <div class="n-search-layout__content bg-green-4">
            <q-scroll-area class="fit q-px-lg">
                <q-scroll-observer @scroll="scrollHandler" />
                <ArticleCard class="q-my-md" v-for="n in 3" />
            </q-scroll-area>
          </div>
        </div>
  </q-layout>
</template>

<style scoped lang="scss">
.n-search-layout {
  display: grid;
  grid-template-rows: auto auto 1fr;
  height: 100vh;
}
.n-search-layout__header {
  grid-area: 1 / 1 / 2 / 3;
}
.n-search-layout__header-stay {
  grid-area: 2 / 1 / 3 / 3;
}
.n-search-layout__content {
  grid-area: 3 / 1 / 4 / 3;
}
</style>
