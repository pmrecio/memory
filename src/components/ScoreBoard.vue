<template>
  <div class="score-board">
    <div>
      <span class="moves">Moves: {{ moves }}</span>
      <span>Discovered: {{ discovered }}</span>
    </div>
    <h2>Lets check your memory!</h2>
    <div>
      <span class="total">Total cards: {{ total }}</span>
      <a @click="updateTotal(total, 2)">+</a>
      <a @click="updateTotal(total, -2)">-</a>
    </div>
  </div>
</template>
<script>
export default {
  name: "ScoreBoard",
  props: {
    total: { Type: Number, default: 10 },
    moves: { Type: Number, default: 0 },
    discovered: { Type: Number, default: 0 },
  },
  methods: {
    updateTotal(total, num) {
      let value = total + num;
      total = value >= 10 && value <= 20 ? value : total;
      this.$emit("update-total", total);
    },
  },
};
</script>

<style scoped>
.score-board {
  background-color: #2196f3;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  width: 100%;
  height: 15px;
  padding: 20px;
  color: white;
}

.moves {
  margin-right: 10px;
}

.total {
  margin: 0 12px 0 0;
}
a {
  cursor: pointer;
  display: inline-block;
  width: 15px;
  height: 15px;
  line-height: 10px;
  border: 1px solid #f5f5f5;
  border-radius: 50%;
  color: #f5f5f5;
  text-align: center;
  text-decoration: none;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
  margin: 0 0 0 5px;
}
</style>
