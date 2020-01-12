<template>
  <div class="board" :style="{ width: state.boardRowItems * 25 + 'px' }">
    <BoardTile v-for="index in state.allBoardItems" :type="getTypeOfCell(index)" :data-key="index" :index="index" />
  </div>
</template>

<script>
import { reactive, computed } from 'vue';
import BoardTile from './BoardTile.vue';
export default {
  setup(props) {
    // Todo: Don't need state here?
    const state = reactive({
      boardRowItems: props.boardRowItems,
      allBoardItems: props.boardRowItems * props.boardRowItems
    });

    // Todo: Move in Config/Props?
    const walls = [17, 24, 33, 37, 55, 58, 74];
    const playerFields = [12, 13, 22, 18, 19, 29, 72, 82, 83, 79, 88, 89];

    const isOnEdge = index => {
      const firstRow = index <= state.boardRowItems;
      const lastRow = state.allBoardItems - index < state.boardRowItems;
      const firstOrLastItemOfRow = index % state.boardRowItems <= 1;

      return firstRow || lastRow || firstOrLastItemOfRow;
    };

    const getTypeOfCell = index => {
      if (isOnEdge(index)) {
        return 'edge';
      }

      if (walls.includes(index)) {
        return 'wall';
      }

      if (playerFields.includes(index)) {
        return 'field';
      }

      return 'destructible';
    };

    return {
      state,
      getTypeOfCell
    };
  },
  components: {
    BoardTile
  },
  props: {
    boardRowItems: Number
  }
};
</script>

<style scoped>
.board {
  display: flex;
  flex-wrap: wrap;
}
</style>
