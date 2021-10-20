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
      :class="{ 'card__img--select': cardIsSelect }"
    />
    <button
      class="card__btn"
      :class="{ 'card__btn--select': cardIsSelect }"
      @click="selectCard"
    >
      {{ textButton }}
    </button>
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
  },
  data() {
    return {
      cardIsSelect: false,
    };
  },
  computed: {
    textButton() {
      return this.cardIsSelect ? "Unselect" : "Select";
    },
  },
  methods: {
    selectCard() {
      this.cardIsSelect = !this.cardIsSelect;
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
  }

  &__img {
    max-width: 97px;
    max-height: 134px;

    &--select {
      width: 55%;
      height: 55%;
    }
  }

  &__btn {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    padding: 6px 24px;
    position: static;
    width: 112px;
    height: 28px;
    left: 40px;
    margin: 12px 0;
    border-radius: 20px;
    border: none;
    background-color: #FFF;
    text-align: center;
    color: #465254;

    &--select {
      font-size: 12px;
      width: 55%;
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
  }
}
</style>
