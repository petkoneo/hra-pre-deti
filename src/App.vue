<template>
  <b-container id="app" fluid="sm">
    <b-row>
      <b-col></b-col>
      <b-col cols="8">
        <b-jumbotron
          header="Skryté číslo"
          lead="Vitajte v hre o chýbajucom čísle"
        >
          <h4>
            Cieľom hry je vypočítať chýbajúce číslo z rovnice uvedenej dole.
            Treba naťukať správne číslo a stlačiť gombík "Zistiť odpoveď". Na
            ďalšiu hru treba stlačiť gombík "Mixuj čísla".
          </h4>
        </b-jumbotron>
        <b-row>
          <b-col> </b-col>
          <b-col cols="8">
            <b-form-group
              id="input-group-1"
              label="Chybajuce cislo:"
              label-for="input-1"
              description="Zadajte sem chybajuce cislo zo vzorca dole."
            >
              <b-form-input
                id="input-1"
                v-model="unknownNum"
                type="number"
                required
                placeholder="Zadajte cislo"
              ></b-form-input>
            </b-form-group>
          </b-col>
          <b-col> </b-col>
        </b-row>
        <b-row style="margin-top: 2rem;" align-h="around">
          <b-button size="lg" @click="testNumbers" variant="success">
            Zistiť odpoveď
          </b-button>

          <b-button size="lg" @click="mixNumbers" variant="danger">
            Mixuj čísla
          </b-button>
        </b-row>
        <b-row style="margin-top: 2rem;" align-h="center">
          <h1>
            {{ firstNum }} +
            <span v-if="unknownNum === null || unknownNum === ''">?</span
            >{{ unknownNum }} = {{ finalNum }}
          </h1>
        </b-row>
      </b-col>
      <b-col></b-col>
    </b-row>
    <b-row style="margin-top: 2rem;">
      <b-col></b-col>
      <b-col cols="8" class="text-center">
        <div v-if="isGood">
          <b-iconstack font-scale="5">
            <b-icon stacked icon="square"></b-icon>
            <b-icon stacked icon="check"></b-icon>
          </b-iconstack>
          <h2 style="align-text: center;">
            Trefa!
          </h2>
        </div>
        <div v-if="isGood === false">
          <b-iconstack font-scale="5">
            <b-icon stacked icon="exclamation-circle"></b-icon>
          </b-iconstack>
          <h2 style="align-text: center;">
            Vedla! Skús znova.
          </h2>
        </div>
      </b-col>
      <b-col></b-col>
    </b-row>
  </b-container>
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

<style lang="scss"></style>
