<template>
  <div>
    <div>{{ turn }}님의 턴입니다.</div>
    <table>
      <tr v-for="(rowData, rowIndex) in tableData" :key="rowIndex">
        <td
          @click="onClickTd(rowIndex, cellIndex)"
          v-for="(cellData, cellIndex) in rowData"
          :key="cellIndex"
        >
          {{ cellData }}
        </td>
      </tr>
    </table>
    <div v-if="winner">{{ winner }}님의 승리!</div>
  </div>
</template>

<script>
import { mapState } from "vuex";
import Vue from "vue";
import TableComponent from "./TableComponent";
import store from "./store";
import {
  CLICK_CELL,
  SET_WINNER,
  RESET_GAME,
  NO_WINNER,
  CHANGE_TURN,
} from "./store";

export default {
  store,
  data() {
    return {
      data: 1,
    };
  },
  components: {
    TableComponent,
  },
  computed: {
    ...mapState(["winner", "turn", "tableData"]),
  },
  methods: {
    onClickTd(rowIndex, cellIndex) {
      if (this.cellData) return;

      this.$store.commit(CLICK_CELL, {
        row: this.rowIndex,
        cell: this.cellIndex,
      });

      //this.$set(this.tableData[rowIndex], [cellIndex], this.turn);

      let win = false;
      if (
        this.tableData[rowIndex][0] === this.turn &&
        this.tableData[rowIndex][1] === this.turn &&
        this.tableData[rowIndex][2] == this.turn
      )
        win = true;
      if (
        this.tableData[0][cellIndex] === this.turn &&
        this.tableData[1][cellIndex] === this.turn &&
        this.tableData[2][cellIndex] === this.turn
      )
        win = true;
      if (
        this.tableData[0][0] === this.turn &&
        this.tableData[1][1] === this.turn &&
        this.tableData[2][2] === this.turn
      )
        win = true;
      if (
        this.tableData[0][2] === this.turn &&
        this.tableData[1][1] === this.turn &&
        this.tableData[2][0] === this.turn
      )
        win = true;

      if (win) {
        this.winner = this.turn;
        this.$store.commit(SET_WINNER, this.turn);
        this.$store.commit(RESET_GAME);
      } else {
        let all = true;
        this.tableData.forEach((row) => {
          row.forEach((cell) => {
            if (!cell) {
              all = false;
            }
          });
        });
        if (all) {
          //무승부/
          this.$store.commit(NO_WINNER);
          this.$store.commit(RESET_GAME);
        } else {
          this.$store.commit(CHANGE_TURN);
        }
      }
    },
  },
  created() {},
};
</script>

<style lang="">
table {
  border-collapse: collapse;
}
td {
  border: 3px solid black;
  width: 200px;
  height: 200px;
  text-align: center;
  transition-duration: 3ms;
}
td:hover {
  transition-duration: 20ms;

  background: #551155;
}
</style>