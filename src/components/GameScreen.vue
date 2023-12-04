<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width: `${
          (((544 / Math.sqrt(cardContext.length) - 16) * 3) / 4 + 16) *
          Math.sqrt(cardContext.length)
        }px`,
      }"
    >
      <card-flip
        v-for="(card, index) in cardContext"
        :key="index"
        :bgImgBack="`images/${card}.png`"
        :cardName="card"
        :indexCard="index"
        :cardContext="cardContext"
        @onFlip="CheckRule($event)"
        :ref="`card-${index}`"
      />
      <!-- <button @click="handleBackToMain" class="">Quay ve</button> -->
    </div>
  </div>
</template>
<script>
import CardFlip from "./CardFlip.vue";

export default {
  name: "GameScreen",
  components: {
    CardFlip,
  },
  emits: ["BackToMain", "EndGame"],
  methods: {
    handleBackToMain() {
      this.$emit("BackToMain");
    },
    CheckRule(CardFlip) {
      if (this.rules.length < 1) this.rules.push(CardFlip);
      if (this.rules.length === 1 && this.rules[0].index !== CardFlip.index)
        this.rules.push(CardFlip);
      // if (this.rules.length > 0) console.log(this.rules);
      if (
        this.rules.length === 2 &&
        this.rules[0].cardName !== this.rules[1].cardName
      ) {
        console.log("Khac");
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onCloseCard();
          this.$refs[`card-${this.rules[1].index}`][0].onCloseCard();
          this.rules = [];
        }, 500);
      }
      if (
        this.rules.length === 2 &&
        this.rules[0].cardName === this.rules[1].cardName
      ) {
        console.log("Giong");
        this.countCard++;
        this.rules = [];
        if (this.countCard === this.cardContext.length / 2) {
          this.$emit("EndGame");
        }
      }
    },
  },
  props: {
    cardContext: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      rules: [],
      countCard: 0,
    };
  },
};
</script>

<style lang="css">
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}
.screen__inner {
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto 1rem;
}
</style>
