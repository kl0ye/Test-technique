<template>
  <div id="app" class="app">
    <nav>
      <button @click="shuffleArray(cardList)">suffle</button>
      <button @click="sortArray()">sort</button>
    </nav>
    <main class="container">
      <h1 class="app__title">Deck of cards</h1>
      <p class="app__sub-title">
        Sed ut perspiciatis unde omnis iste natus error sit voluptatem
        accusantium doloremque
      </p>
      <p class="cards-container__nb-select">
        Carte selectionné : {{ nbCArdSelect }}
      </p>
      <div class="cards-container">
        <div v-for="(card, index) in cardList" :key="index" class="cards">
          <Card
            class="card-item"
            :name="card.name"
            :suit="card.suit"
            :image="card.image"
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
    nbCArdSelect() {
      return this.cardSelectedList.length;
    },
  },
  mounted() {
    this.cardList = [...cardListJson];
  },
  methods: {
    cardSelected(card) {
      if (this.cardSelectedList.find((item) => item === card)) {
        return (this.cardSelectedList = this.cardSelectedList.filter(
          (item) => item !== card
        ));
      }
      return this.cardSelectedList.push(card);
    },
    shuffleArray(array) {
      array.sort(() => Math.random() - 0.5);
    },
    sortArray() {
      this.cardList = [...cardListJson];
    },
  },
};
</script>

<style lang="scss">
.app {
  background: #F5F7F7;
  font-family: Work Sans;
  font-style: normal;
  font-size: 14px;
  font-weight: 600;
  line-height: 16px;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.app {
  &__title {
    font-weight: bold;
    font-size: 32px;
    line-height: 38px;
    color: #465254;
    text-align: center;
  }

  &__sub-title {
    font-weight: 500;
    font-size: 20px;
    line-height: 23px;
    color: #465254;
    text-align: center;
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

@media (min-width: 680px) {
  .card-item {
    margin-bottom: 32px;
  }

  .cards-container {
    grid-template-columns: 1fr 1fr 1fr 1fr;
    max-width: 972px;
    margin: auto;
  }
}
</style>
