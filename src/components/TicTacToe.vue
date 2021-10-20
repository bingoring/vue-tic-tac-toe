<template>
  <table-component v-bind:table-data="tableData"></table-component>
</template>

<script>
import TableComponent from './TableComponent';
export default {
  components: {
    TableComponent,
  },
  data() {
    return {
      tableData: [
        ['','',''],
        ['','',''],
        ['','','']
      ],
      turn : 'O',
    };
  },
}
</script>

<style lang="">
table{
  border-collapse: collapse;
}
td { 
  border: 1px solid black;
  width: 40p;
  height: 40px;
  text-align: center;
}
</style>