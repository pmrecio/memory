<template>
    <div :class="[card.active ? 'card' : '', 'card-body']">
        <a @click="discover(card, index)" v-if="card.active">
            <img class="card-image" :src="getImgUrl(card)" />
        </a>
    </div>
</template>

<script>
export default {
    name: 'CardItem',
    data() {
        return { chance: 0 };
    },
    props: { card: Object, index: Number },
    methods: {
        /**
         * Change the visible stage of the card and execute play the game method.
         */
        discover(card, index) {
            card.visble = true;
            this.$emit('play-game', index);
        },

        /**
         * Get the correct url for the card image.
         */
        getImgUrl(card) {
            let name = !card.visble
                ? 'card-background'
                : card.value.toLowerCase();
            const images = require.context(
                '../assets/images/',
                false,
                /\.png$/
            );
            return images('./' + name + '.png');
        },
    },
};
</script>

<style scoped>
a {
    cursor: pointer;
}

.card-body {
    margin: 0.5rem;
    border-radius: 10px;
    width: 170px;
    height: 200px;
    transition: 0.3s;
    padding: 10px;
}

.card {
    background-color: #fff;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);

    font-size: 30px;
    text-align: center;
}

.card:hover {
    box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}

.card-image {
    width: 170px;
    height: 200px;
}
</style>
