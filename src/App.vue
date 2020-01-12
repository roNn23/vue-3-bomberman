<template>
  <button @click="showHelloWorld">
    Click for Hello World!
  </button>
  <div v-if="state.clicked">
    <h1>Hello World 💣</h1>
  </div>
</template>

<script>
import { reactive, computed } from 'vue';
export default {
  setup() {
    const state = reactive({
      clicked: false
    });

    const showHelloWorld = () => {
      state.clicked = true;
    };

    return {
      state,
      showHelloWorld
    };
  }
};
</script>

<style scoped>
h1 {
  font-family: Arial, Helvetica, sans-serif;
}
</style>
