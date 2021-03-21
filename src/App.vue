<template>
  <h3>TV Finder</h3>
  <render-me>
    <!-- <template #namedSlot>
          <h3>Hello From Named Slot</h3>
        </template> -->
    <!-- <h4>Hi From Default slot</h4> -->
    <template #sc="{ shows }">
      <h3 v-if="shows?.length > 0">
        Average Score {{ computedAverage(shows).toFixed(2) }}
      </h3>
    </template>
  </render-me>

  <heading>Hi From ThiS heading</heading>
</template>

<script setup>
import RenderMe from "./components/RenderMe.vue";
import Heading from "./components/Heading.vue";

const computedAverage = (shows) =>
  shows.reduce((acc, info) => +info.score + acc, 0) / shows.length;

// This starter template is using Vue 3 experimental <script setup> SFCs
// Check out https://github.com/vuejs/rfcs/blob/script-setup-2/active-rfcs/0000-script-setup.md
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
