<template>
  <div class="screen">
    <h1>Game Pokemon</h1>
    <p>Select mode</p>
    <div class="modes">
      <button @click="SelectGame(16)">
        <span>4x4</span>
        <span>Dễ</span>
      </button>
      <button @click="SelectGame(36)">
        <span>6x6</span>
        <span>Thường</span>
      </button>
      <button @click="SelectGame(64)">
        <span>8x8</span>
        <span>Khó</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainScreen",
  emits: ["SelectModeGame"],
  methods: {
    SelectGame(totalOfBlocks) {
      this.$emit("SelectModeGame", { totalOfBlocks });
    },
  },
};
</script>

<style scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
}
.screen h1 {
  font-size: 4.5rem;
  text-transform: uppercase;
}

.screen p {
  font-size: 2rem;
}

.modes {
  display: flex;
  margin-top: 2rem;
}

.modes button {
  font: var(--font);
  width: 150px;
  height: 150px;
  background: transparent;
  box-shadow: none;
  border: 1px solid var(--light);
  color: var(--light);
  display: flex;
  flex-direction: column;
  border-radius: 1rem;
  margin: 0 1rem;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: background 0.3s ease-in-out;
}

.modes button:hover {
  background-color: var(--light);
  color: var(--dark);
}

.modes button span:first-child {
  font-size: 2rem;
}

.modes button span:last-child {
  display: block;
  font-size: 1.25rem;
  margin-top: 0.5rem;
}
</style>
