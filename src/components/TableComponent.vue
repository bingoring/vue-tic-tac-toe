<template>
  <table>
    <tr-component
      v-for="(rowData, index) in tableData"
      :row-data="rowData"
      :row-index="index"
      :turn="turn"
      :key="index"
    ></tr-component>
  </table>
</template>

<script>
import TrComponent from "./TrComponent";
export default {
  props: {
    tableData: Array,
    turn: String,
  },
  computed: {
    tableData() {
      return this.$store.state.tableData;
    },
  },
  components: {
    TrComponent,
  },
};
</script>

<style lang="">
</style>