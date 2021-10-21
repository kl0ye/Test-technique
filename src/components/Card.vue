<template>
  <div
    class="card"
    :class="[`card--${suit}`, { 'card--select': cardIsSelect }]"
  >
    <h2 class="card__title" :class="{ 'card__title--select': cardIsSelect }">
      {{ name }}
    </h2>
    <img
      :src="image"
      class="card__img"
      :alt="`card ${name} of ${suit}`"
      :class="{ 'card__img--select': cardIsSelect }"
    />
    <div class="card__btn-container">
      <button
        class="card__btn"
        :class="{ 'card__btn--select': cardIsSelect }"
        @click="selectCard"
      >
        {{ textButton }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    name: {
      type: String,
      required: true,
    },
    suit: {
      type: String,
      required: true,
    },
    image: {
      type: String,
      required: true,
    },
    cardIsSelect: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    textButton() {
      return this.cardIsSelect ? "Unselect" : "Select";
    },
  },
  methods: {
    selectCard() {
      this.$emit("card-selected");
    },
  },
};
</script>

<style lang="scss">
.card {
  width: 161px;
  height: 232px;
  border-radius: 3px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  box-shadow: 0px 11px 23px rgba(0, 0, 0, 0.5);
  border-radius: 3px;

  &--hearts,
  &--diamonds {
    background-color: #E32A00;
  }

  &--spades,
  &--clubs {
    background-color: #1E2324;
  }

  &--select {
    opacity: 0.7;
    max-width: 80%;
    max-height: 80%;
  }

  &__title {
    font-weight: bold;
    color: #fff;
    font-size: 16px;
    line-height: 19px;
    margin: 0;
  }

  &__img {
    max-width: 97px;
    max-height: 134px;
    margin: 12px;

    &--select {
      width: 55%;
      height: 55%;
    }
  }

  &__btn {
    display: flex;
    font-weight: bold;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    padding: 6px 24px;
    position: static;
    width: 97px;
    height: 28px;
    left: 40px;
    border-radius: 20px;
    border: none;
    background-color: #FFF;
    text-align: center;
    color: #465254;
    overflow: hidden;

    &-container {
      position: relative;
    }

    &--select {
      font-size: 12px;
    }

    &::before {
      content: "";
      position: absolute;
      left: 0;
      height: 28px;
      width: 30%;
      border-radius: 20px;
      background-color: transparent;
      transition: 1s all ease;
    }

    &::after {
      transition: 1.5s all ease;
    }
  }

  &__btn:hover {
    &::before {
      width: 100.5%;
      background-color: #2ABA7E;
      transition: 1s all ease;
    }

    &::after {
      content: "Select";
      position: absolute;
      color: #FFF;
      transition: 1s all ease;
    }
  }

  &__btn--select:hover {
    &::after {
      content: "Unselect";
    }
  }
}

@media (min-width: 680px) {
  .card {
    width: 192px;
    height: 276px;

    &__img {
      max-width: 112px;
      max-height: 157px;
    }

    &__btn {
      width: 112px;
    }
  }
}
</style>
