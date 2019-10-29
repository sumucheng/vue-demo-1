<template>
  <div class="wrapper">
    <div class="panel">
      <div>第{{n}}手</div>
      <div>{{result===null?'':`胜利者：${result}`}}</div>
    </div>
    <div class="chess">
      <div class="row">
        <Cell @click="onClickCell(0,$event)" :n="n" />
        <Cell @click="onClickCell(1,$event)" :n="n" />
        <Cell @click="onClickCell(2,$event)" :n="n" />
      </div>
      <div class="row">
        <Cell @click="onClickCell(3,$event)" :n="n" />
        <Cell @click="onClickCell(4,$event)" :n="n" />
        <Cell @click="onClickCell(5,$event)" :n="n" />
      </div>
      <div class="row">
        <Cell @click="onClickCell(6,$event)" :n="n" />
        <Cell @click="onClickCell(7,$event)" :n="n" />
        <Cell @click="onClickCell(8,$event)" :n="n" />
      </div>
    </div>
  </div>
</template>

<script>
import Cell from "./Cell";
export default {
  components: { Cell },
  data() {
    return {
      n: 0,
      map: [[null, null, null], [null, null, null], [null, null, null]],
      result: null
    };
  },
  methods: {
    onClickCell(i, text) {
      this.map[Math.floor(i / 3)][i % 3] = text;
      this.n = this.n + 1;
      this.tell();
    },
    tell() {
      for (let i = 0; i < 3; i++) {
        if (
          this.map[i][0] !== null &&
          this.map[i][0] === this.map[i][1] &&
          this.map[i][1] === this.map[i][2]
        ) {
          this.result = this.map[i][0];
        }
      }
      for (let j = 0; j < 3; j++) {
        if (
          this.map[0][j] !== null &&
          this.map[0][j] === this.map[1][j] &&
          this.map[1][j] === this.map[2][j]
        ) {
          this.result = this.map[0][j];
        }
      }
      if (
        this.map[0][0] !== null &&
        this.map[0][0] === this.map[1][1] &&
        this.map[1][1] === this.map[2][2]
      ) {
        this.result = this.map[0][0];
      }
      if (
        this.map[0][2] !== null &&
        this.map[0][2] === this.map[1][1] &&
        this.map[1][1] === this.map[2][0]
      ) {
        this.result = this.map[0][2];
      }
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}
.row {
  display: flex;
}
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}
.panel {
  margin-right: 30px;
  background-color: bisque;
  width: 100px;
  height: 100px;
  text-align: center;
  padding-top: 20px;
}
</style>
