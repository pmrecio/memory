<template>
  <div class="winner-board">
    <h2>
      You won! <span class="moves">Moves: {{ moves }}</span>
      <span>Total cards: {{ total }}</span>
    </h2>
    <img src="../assets/images/animals.png" />
  </div>
</template>

<script>
export default {
  name: "WinnerBoard",
  props: { moves: Number, total: Number },
};
</script>

<style scoped>
.moves {
  margin: 0 15px;
}
img {
  width: 75%;
}
h2 {
  color: #2196f3;
  font-size: 2rem;
}
</style>
