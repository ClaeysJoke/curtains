<template>
  <div class="hello">
    <h1>Overgordijnen</h1>
    <b-row style="margin-bottom: 5rem">
      <b-col>
        <b-form-group>
          <b-form-radio v-model="roomHigh" :value="true"
            >kamerhoog</b-form-radio
          >
          <b-form-radio v-model="roomHigh" :value="false">1.40m</b-form-radio>
        </b-form-group>
      </b-col>
      <b-col>
        <b-form-group>
          <b-form-radio v-model="withPrint" :value="true"
            >met tekening</b-form-radio
          >
          <b-form-radio v-model="withPrint" :value="false">effen</b-form-radio>
        </b-form-group>
      </b-col>
    </b-row>
    <b-row>
      <b-col cols="2">
        <label>Hoogte raam </label>
      </b-col>
      <b-col>
        <b-form-input
          style="max-width: 15rem"
          v-model="hight"
          type="number"
        ></b-form-input>
      </b-col>
    </b-row>
    <b-row>
      <b-col cols="2">
        <label>Breedte raam </label>
      </b-col>
      <b-col>
        <b-form-input
          style="max-width: 15rem"
          v-model="width"
          type="number"
        ></b-form-input>
      </b-col>
    </b-row>
    <b-row v-if="withPrint">
      <b-col cols="2">
        <label>Hoogte tekening </label>
      </b-col>
      <b-col>
        <b-form-input
          style="max-width: 15rem"
          v-model="hightPrint"
          type="number"
        ></b-form-input>
      </b-col>
    </b-row>
    <b-row></b-row>
    <b-row v-if="result != 0 && result != Infinity">
      <b-col cols="2">
        <label v-if="!withPrint"> Aantal meter stof nodig </label>
        <label v-if="withPrint"> Aantal tekeningen </label>
      </b-col>
      <b-col style="max-width: 15rem">
        {{ result }}
      </b-col>
    </b-row>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Curtains extends Vue {
  public noSecondLayer: boolean = true;
  public roomHigh: boolean = true;
  public withPrint: boolean = true;

  public width: number = 0;
  public hight: number = 0;
  public hightPrint: number = 0;

  public get result(): number {
    var fabricInM = 0;
    if (!this.roomHigh) {
      var nrPanden = (this.width * 2) / 1.4;
      fabricInM = nrPanden * (this.hight + 30);
    } else {
      fabricInM = this.width * 2 + 20;
    }

    if (!this.withPrint) {
      return fabricInM;
    } else {
      return Math.ceil(fabricInM / this.hightPrint) + 1;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
