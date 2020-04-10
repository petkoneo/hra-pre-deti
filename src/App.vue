<template>
  <div id="app">
    <div class="main">
      <h1>Vitajte v chybajucom cisle</h1>
      <input type="number" v-model="unknownNum" />
      <button @click="testNumbers">Stlac odpoved</button>
      <button @click="mixNumbers">Stlac Mixuj</button>
      <div class="numbers">
        <h1>{{ firstNum }} + {{ unknownNum }} = {{ finalNum }}</h1>
      </div>
      <div v-if="isGood">
        <h2>Trafil si uc sa</h2>
      </div>
      <div v-if="isGood === false">
        <h2>Netrafil si uc SA</h2>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      firstNum: 0,
      unknownNum: null,
      finalNum: 0,
      isGood: null
    };
  },
  methods: {
    getRandomInt(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min)) + min; //The maximum is exclusive and the minimum is inclusive
    },
    mixNumbers() {
      this.isGood = null;
      this.firstNum = this.getRandomInt(1, 50);
      this.finalNum = this.getRandomInt(51, 100);
      this.unknownNum = null;
    },
    testNumbers() {
      const sum = Number(this.firstNum) + Number(this.unknownNum);

      if (sum === this.finalNum) {
        this.isGood = true;
      } else {
        this.isGood = false;
      }
    }
  },
  created() {
    this.mixNumbers();
  }
};
</script>

<style lang="scss">
#app {
  width: 100vw;
  height: 100vh;

  div.main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    .numbers {
    }
  }
}
</style>
