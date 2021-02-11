<template>
  <div id="app">
    <div class="counter">
      <h1>
        {{ counter }}
      </h1>
    </div>

    <section class="memory-game">
      <div
        class="memory-card"
        v-for="(card, index) in cards"
        :key="index"
        :data-framework="card.name"
        @click="flipCard(index)"
        :class="{ flip: card.flipped, 'disable-card': card.disabled }"
      >
        <img
          class="front-face"
          :src="require(`../src/assets/img/${card.name}.svg`)"
          :alt="card.name"
        />
        <img
          class="back-face"
          src="../src/assets/img/js-badge.svg"
          alt="JS Badge"
        />
      </div>
    </section>
  </div>
</template>

<script>
let interval;
const secondsToEnd = 60;
export default {
  data() {
    return {
      counter: secondsToEnd,
      selectedCards: [],
      points: 0,
      cards: [
        {
          name: "angular",
          flipped: false,
          disabled: false,
        },
        {
          name: "aurelia",
          flipped: false,
          disabled: false,
        },
        {
          name: "backbone",
          flipped: false,
          disabled: false,
        },
        {
          name: "ember",
          flipped: false,
          disabled: false,
        },
        {
          name: "react",
          flipped: false,
          disabled: false,
        },
        {
          name: "vue",
          flipped: false,
          disabled: false,
        },
        {
          name: "angular",
          flipped: false,
          disabled: false,
        },
        {
          name: "aurelia",
          flipped: false,
          disabled: false,
        },
        {
          name: "backbone",
          flipped: false,
          disabled: false,
        },
        {
          name: "ember",
          flipped: false,
          disabled: false,
        },
        {
          name: "react",
          flipped: false,
          disabled: false,
        },
        {
          name: "vue",
          flipped: false,
          disabled: false,
        },
      ],
    };
  },
  watch: {
    selectedCards() {
      if (this.selectedCards.length % 2 == 0 && this.selectedCards.length > 0) {
        let firstIndex = this.selectedCards[0];
        let secondIndex = this.selectedCards[1];
        if (this.cards[firstIndex].name == this.cards[secondIndex].name) {
          this.cards[firstIndex].disabled = true;
          this.cards[secondIndex].disabled = true;
          this.points += 2;
        } else {
          setTimeout(() => {
            this.cards[firstIndex].flipped = false;
            this.cards[secondIndex].flipped = false;
          }, 500);
        }
        this.selectedCards = [];
      }
    },
    counter() {
      if (this.counter == 0) {
        this.endGame("lost");
      }
    },
    points() {
      if (this.points == this.cards.length) {
        this.endGame("win");
      }
    },
  },
  computed: {},
  methods: {
    flipCard(index) {
      let selectedCard = this.cards[index];
      selectedCard.flipped = !selectedCard.flipped;
      if (selectedCard.flipped) {
        this.selectedCards.push(index);
      }
    },
    randomizeCards() {
      var currentIndex = this.cards.length,
        temporaryValue,
        randomIndex;

      // While there remain elements to shuffle...
      while (0 !== currentIndex) {
        // Pick a remaining element...
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        // And swap it with the current element.
        temporaryValue = this.cards[currentIndex];
        this.cards[currentIndex] = this.cards[randomIndex];
        this.cards[randomIndex] = temporaryValue;
      }
      this.cards = [...this.cards];
      interval = setInterval(() => {
        this.counter--;
      }, 1000);
    },
    endGame(winLost) {
      this.cards.forEach((card) => {
        card.flipped = false;
        card.disabled = false;
      });

      confirm(`You ${winLost}!`);
      clearInterval(interval);
      this.counter = secondsToEnd;
      this.randomizeCards();
      this.selectedCards = [];
    },
  },
  mounted() {
    this.randomizeCards();
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  height: 100vh;
  display: flex;
  background-image: linear-gradient(120deg, #d4fc79 0%, #96e6a1 100%);
}

#app {
  width: 100%;
  padding: 7%;
}
.memory-game {
  width: 640px;
  height: 640px;
  margin: auto;
  display: flex;
  flex-wrap: wrap;
  perspective: 1000px;
}

.memory-card {
  width: calc(25% - 10px);
  height: calc(33.333% - 10px);
  margin: 5px;
  position: relative;
  transform: scale(1);
  transform-style: preserve-3d;
  transition: transform 0.5s;
  box-shadow: 1px 1px 1px rgba(0, 0, 0, 0.3);
}

.disable-card {
  pointer-events: none;
}

.memory-card:active {
  transform: scale(0.97);
  transition: transform 0.2s;
}

.memory-card.flip {
  transform: rotateY(180deg);
}

.front-face,
.back-face {
  width: 100%;
  height: 100%;
  padding: 20px;
  position: absolute;
  border-radius: 5px;
  background: #fff29e;
  backface-visibility: hidden;
}

.front-face {
  transform: rotateY(180deg);
}

.counter {
  position: absolute;
  top: 0px;
  right: 0px;
}
</style>
