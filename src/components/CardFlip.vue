<template>
  <div
    class="card"
    :class="{ disabled: isFlipped }"
    :style="{
      width: `${((544 / Math.sqrt(cardContext.length) - 16) * 3) / 4}px`,
      height: `${544 / Math.sqrt(cardContext.length) - 16}px`,
    }"
  >
    <div
      class="card__inner"
      :class="{ 'is-Flip': isFlipped }"
      @click="onToggleCardFlip"
    >
      <div class="card__face card__face--front">
        <div class="card__content"></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + bgImgBack)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardFlip",
  props: {
    bgImgBack: {
      type: String,
      required: true,
    },
    cardName: {
      type: [String, Number, Object, Array],
    },
    indexCard: {
      type: [String, Number, Object, Array],
    },
    cardContext: {
      type: Array,
    },
  },
  data() {
    return {
      isFlipped: false,
      widthCard: Math.sqrt(this.cardContext.length),
    };
  },
  methods: {
    onToggleCardFlip() {
      if (this.isFlipped) return false;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped)
        this.$emit("onFlip", {
          index: this.indexCard,
          cardName: this.cardName,
        });
    },
    onCloseCard() {
      this.isFlipped = false;
    },
  },
};
</script>

<style lang="css" scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
}

.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}

.card.disabled .card__inner {
  cursor: default;
}

.card__inner.is-Flip {
  transform: rotateY(-180deg);
}

.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  padding: 0.5rem;
  border-radius: 0.5rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.3);
}

.card__face--front .card__content {
  background: url(../assets/images/icon_back.png) no-repeat center center;
  background-size: contain;
  height: 100%;
  width: 100%;
}

.card__face--back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}

.card__face--back .card__content {
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}
</style>
