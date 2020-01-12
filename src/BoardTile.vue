<template>
  <div class="board-tile" :class="type"></div>
</template>

<script>
export default {
  props: {
    type: String,
    index: Number
  }
};
</script>

<style scoped>
.board-tile {
  width: 25px;
  height: 25px;
}

.edge {
  background: darkgray;
  border: 1px solid white;
  width: 23px;
  height: 23px;
}

.wall {
  background: lightgray;
}

.field {
  background: green;
}

.destructible {
  background: brown;
}
</style>
