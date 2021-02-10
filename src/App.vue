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
export default {
  data() {
    return {
      counter: 60,
      selectedCards: [],
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
    // cards() {
    //   this.cards.forEach((card) => {
    //   });
    // },
    selectedCards() {
      if (this.selectedCards.length == this.cards.length) {
        setTimeout(() => {
          this.cards.forEach((card) => {
            card.flipped = false;
            card.disabled = false;
          });
          console.log(this.cards);
          this.randomizeCards();
          this.selectedCards = [];
          confirm("finished");
        }, 500);
      } else if (
        this.selectedCards.length % 2 == 0 &&
        this.selectedCards.length > 0
      ) {
        this.selectedCards.forEach((card) => {
          //let firstValue;
          //let secondValue;
          if (!card.disabled) {
            let secondIndex = this.selectedCards.indexOf(card);
            console.log(secondIndex);
            console.log(this.selectedCards);
            let firstValue = this.selectedCards[secondIndex + 1];
            console.log(firstValue);
            console.log(card);
            if (firstValue && firstValue.name !== card.name) {
              this.cards.forEach((card) => {
                setTimeout(() => {
                  console.log(card.disabled);
                  if (!card.disabled) {
                    console.log("FLIPPPPP");
                    card.flipped = false;
                  }
                }, 500);
                //card.flipped = false;
              });
              this.cards = [...this.cards];
              this.selectedCards = [];
            }
          } else {
            this.cards.forEach((card) => {
              if (card.flipped) {
                setTimeout(() => {
                  console.log("DISABLEDDDDD");
                  card.disabled = true;
                }, 500);
              }
            });
          }
        });

        // let firstValue = this.selectedCards[0];
        // let secondValue = this.selectedCards[1];
        // console.log(this.selectedCards[0]);
        // console.log(this.selectedCards[1]);
        // this.selectedCards.map((card) => {
        //   console.log("from map ");
        //   console.log(card);
        // });
        // if (firstValue.name !== secondValue.name) {
        //   this.cards.forEach((card) => {
        //     setTimeout(() => {
        //       card.flipped = false;
        //     }, 500);
        //     //card.flipped = false;
        //   });
        //   this.cards = [...this.cards];
        //   this.selectedCards = [];
        // } else {
        //   this.cards.forEach((card) => {
        //     if (card.flipped) {
        //       setTimeout(() => {
        //         console.log("DISABLEDDDDD");
        //         card.disabled = true;
        //       }, 500);
        //     }
        //   });
        // }
      }
      console.log(this.selectedCards.length);
    },
  },
  computed: {
    // counter() {
    //   let count = 60;
    //   setTimeout((count) => {
    //     if (count >= 0) {
    //       count--;
    //     }
    //   }, 1000);
    //   return count;
    // },
  },
  methods: {
    flipCard(index) {
      let selectedCard = this.cards[index];
      selectedCard.flipped = !selectedCard.flipped;
      let indexIfAlreadySelected = this.selectedCards.indexOf(selectedCard);
      if (selectedCard.flipped && indexIfAlreadySelected == -1) {
        this.selectedCards.push(selectedCard);
      } else if (!selectedCard.flipped && indexIfAlreadySelected != -1) {
        this.selectedCards.splice(indexIfAlreadySelected, 1);
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
