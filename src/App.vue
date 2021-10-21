<template>
  <div id="app" class="app">
    <nav class="app__nav-bar">
      <button
        class="app__btn app__btn--primary"
        @click="shuffleArray(cardList)"
      >
        <img src="./assets/suffle.svg" alt="" />
        Suffle
      </button>
      <button class="app__btn app__btn--secondary" @click="sortArray()">
        Sort
      </button>
    </nav>
    <main class="app__container">
      <h1 class="app__title">Deck of cards</h1>
      <p class="app__sub-title">
        Sed ut perspiciatis unde omnis iste natus error sit voluptatem
        accusantium doloremque
      </p>
      <p class="app__text">Number of cards selected : {{ nbCardSelect }}</p>
      <p class="app__text">Total value : {{ totalValue }}</p>
      <div class="cards-container">
        <div v-for="(card, index) in cardList" :key="index" class="cards">
          <Card
            class="card-item"
            :name="card.name"
            :suit="card.suit"
            :image="card.image"
            :card-is-select="card.select"
            @card-selected="cardSelected(card)"
          />
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import Card from "./components/Card";
import cardListJson from "./json/cardList.json";

export default {
  name: "App",
  components: {
    Card,
  },
  data() {
    return {
      cardList: [],
      cardSelectedList: [],
    };
  },
  computed: {
    nbCardSelect() {
      return this.cardSelectedList.length;
    },
    totalValue() {
      const allCardValue = this.cardSelectedList.map((item) => item.value);
      return allCardValue.length > 0 ? allCardValue.reduce(this.reducer) : 0;
    },
  },
  mounted() {
    this.cardList = [...cardListJson];
    this.cardList.forEach((card) => {
      card.select = false;
      card.value = this.mapValue(card.name);
    });
  },
  methods: {
    reducer: (accumulator, currentValue) => accumulator + currentValue,
    cardSelected(card) {
      this.cardList.forEach((item) => {
        if (item === card) {
          item.select = !card.select;
        }
      });
      this.putInSelectCardArray(card);
    },
    putInSelectCardArray(card) {
      if (this.cardSelectedList.find((item) => item === card)) {
        return (this.cardSelectedList = this.cardSelectedList.filter(
          (item) => item !== card
        ));
      }
      return this.cardSelectedList.push(card);
    },
    shuffleArray(array) {
      this.resetSelectCard();
      array.sort(() => Math.random() - 0.5);
    },
    sortArray() {
      this.resetSelectCard();
      this.cardList = [...cardListJson];
    },
    resetSelectCard() {
      this.cardSelectedList = [];
      this.cardList.forEach((item) => {
        if (item.select === true) {
          item.select = false;
        }
      });
    },
    mapValue(cardName) {
      switch (cardName) {
        case "Ace":
          return 1;
        case "Jack":
          return 11;
        case "Queen":
          return 12;
        case "King":
          return 13;
        default:
          return parseInt(cardName, 10);
      }
    },
  },
};
</script>

<style lang="scss">
.app {
  background: #F5F7F7;
  font-family: Work Sans;
  font-style: normal;
  font-weight: 500;
  font-size: 14px;
  line-height: 16px;

  &__nav-bar {
    position: fixed;
    z-index: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 73px;
    width: 100%;
    background-color: #FFF;
    box-shadow: 0px 0px 8px rgba(30, 35, 36, 0.16);
  }

  &__container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding-top: 73px;
  }

  &__title {
    font-weight: bold;
    font-size: 32px;
    line-height: 38px;
    color: #465254;
    text-align: center;
  }

  &__sub-title {
    font-size: 16px;
    line-height: 19px;
    color: #465254;
    text-align: center;
  }

  &__text {
    text-align: center;
    margin-top: 0;
  }

  &__btn {
    border: none;
    padding: 8px 16px;
    border-radius: 8px;
    font-weight: 600;
    font-size: 16px;
    line-height: 19px;
    margin: 0 6px;

    &--primary {
      background-color: #099AF2;
      color: #FFF;
    }

    &--secondary {
      background: #D5EEFD;
      color: #0773B5;
    }

    &--primary:hover,
    &--secondary:hover {
      opacity: 0.8;
    }
  }
}

.cards {
  display: flex;
  align-items: center;
  justify-content: center;

  &-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    margin: auto;
  }
}
.card {
  margin: 0 12px;

  &-item {
    margin-bottom: 24px;
  }
}
@media (min-width: 850px) {
  .cards-container {
    grid-template-columns: 1fr 1fr 1fr;
  }

  .app {
    &__nav-bar {
      width: 200px;
      height: 100%;
      position: fixed;
      overflow: auto;
      box-shadow: none;
      flex-direction: column;
    }

    &__btn,
    &__sub-title {
      font-size: 20px;
      line-height: 23px;
    }

    &__btn {
      padding: 12px 16px;
      margin: 5px 0;
    }

    &__container {
      padding-top: 0;
      padding-left: 200px;
    }
  }

  .card-item {
    margin-bottom: 32px;
  }
}

@media (min-width: 1061px) {
  .cards-container {
    grid-template-columns: 1fr 1fr 1fr 1fr;
    max-width: 972px;
    margin: auto;
  }
}
</style>
