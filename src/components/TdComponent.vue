<template>
  <td @click="onClickTd">
    {{ cellData }}
  </td>
</template>

<script>
import { mapState } from "vuex";
import {
  CLICK_CELL,
  SET_WINNER,
  RESET_GAME,
  NO_WINNER,
  CHANGE_TURN,
} from "./store";

export default {
  props: {
    cellData: String,
    rowIndex: Number,
    cellIndex: Number,
  },
  computed: {
    ...mapState({
      tableData: (state) => state.tableData,
      turn: (state) => state.turn,
      cellData(state) {
        return state.tableData[this.rowIndex][this.cellIndex];
      },
    }),
  },
  methods: {
    onClickTd() {
      if (this.cellData) return;

      this.$store.commit(CLICK_CELL, {
        row: this.rowIndex,
        cell: this.cellIndex,
      });

      //this.$set(this.tableData[rowIndex], [cellIndex], this.turn);

      let win = false;
      if (
        this.tableData[this.rowIndex][0] === this.turn &&
        this.tableData[this.rowIndex][1] === this.turn &&
        this.tableData[this.rowIndex][2] == this.turn
      )
        win = true;
      if (
        this.tableData[0][this.cellIndex] === this.turn &&
        this.tableData[1][this.cellIndex] === this.turn &&
        this.tableData[2][this.cellIndex] === this.turn
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
      //EventBus.$emit("clickTd", this.rowIndex, this.cellIndex);
    },
  },
};
</script> 