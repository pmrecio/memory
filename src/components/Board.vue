<template>
    <div id="card-container" class="card-container">
        <Card
            :key="card.id"
            v-for="(card, index) in cards"
            :card="card"
            :index="index"
            @play-game="$emit('play-game', index)"
        ></Card>
    </div>
</template>

<script>
import Card from './Card.vue';

export default {
    name: 'BoardItem',
    components: { Card },
    emit: ['play-game'],
    props: { cards: { Type: Array, default: [] } },
};
</script>

<style scoped>
.card-container {
    display: grid;
    grid-template-columns: auto auto auto auto auto;
    background-color: #2196f3;
    padding: 10px;
}
</style>
