<template>
  <div>
    <ScoreBoard
      :total="total"
      :moves="moves"
      :discovered="discovered"
      @update-total="updateTotal"
    />
    <div class="board">
      <h1>MEMORY</h1>
      <WinnerBoard
        v-if="total / 2 == discovered"
        :moves="moves"
        :total="total"
      />
      <Board
        :cards="cards"
        @play-game="playGame"
        v-if="total / 2 != discovered"
      />
    </div>
  </div>
</template>

<script>
import ScoreBoard from "./components/ScoreBoard";
import Board from "./components/Board";
import WinnerBoard from "./components/WinnerBoard";

export default {
  name: "app",
  components: { ScoreBoard, Board, WinnerBoard },
  data() {
    return {
      cards: [],
      chance: 0,
      previous: null,
      total: 10, //total of card to be play.
      moves: 0,
      discovered: 0,
    };
  },
  created() {
    this.cards = this.generateGroupOfCards(this.total);
  },
  methods: {
    updateTotal(value) {
      this.total = value;
      this.discovered = 0;
      this.moves = 0;
      this.cards = this.generateGroupOfCards(this.total);
    },
    /**
     * Play the game using the position of the card that is seeing.
     */
    playGame(index) {
      //keep track of the chances for discovering cards
      ++this.chance;

      if (this.chance == 2) {
        this.moves++;
        //if the values of the cards are the same change the active status to false.
        if (this.cards[this.previous].value == this.cards[index].value) {
          this.discovered++;

          this.cards[this.previous].active = false;
          this.cards[index].active = false;
        } else {
          //otherwise change the visible stage of the card
          setTimeout(() => {
            this.cards = this.cards.map((card) => {
              card.visble = false;
              return card;
            });
          }, 750);
        }

        this.chance = 0; // reset the chance.
      }

      this.previous = index; // save the privius index.
    },
    /**
     * Generate the card randomly using a predefined array with the values.
     */
    generateGroupOfCards(totalCards) {
      //values to generate the array
      const CARDS_VALUES = [
        "ALLIGATOR",
        "BEAR",
        "COW",
        "DOG",
        "ELEPHANT",
        "FOX",
        "GIRAFFE",
        "HORSE",
        "IGUANA",
        "JELLYFISH",
        "KOALA",
        "LION",
        "MONKEY",
        "NEWT",
        "OWL",
        "PIG",
        "QUAIL",
        "RACOON",
        "SEAGULL",
        "TIGER",
        "VULTURE",
        "URCHIN",
        "WHALE",
        "X-RAY",
        "YAHK",
        "ZEBRA",
      ];

      //Generate ramdon set of cards from the cards values
      let set = [];
      totalCards = totalCards / 2;
      while (totalCards > 0) {
        const random = Math.floor(Math.random() * CARDS_VALUES.length);
        set.push(CARDS_VALUES[random]);
        totalCards--;
      }

      //create the matching card
      set = set.concat(set);
      set.sort(() => Math.random() - 0.5);
      let cards = [];
      let id = 0;
      set.forEach((element) => {
        cards.push({
          id: ++id,
          active: true,
          visble: false,
          value: element,
        });
      });

      return cards;
    },
  },
};
</script>

<style>
body {
  background-color: #fff;
  color: #000;
  font-family: "Dosis", Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin: 0px;
}

.board {
  margin: 0 auto;
  max-width: 75%;
  color: #34495e;
}

h1 {
  text-transform: uppercase;
  font-weight: bold;
  font-size: 3em;
}
</style>
