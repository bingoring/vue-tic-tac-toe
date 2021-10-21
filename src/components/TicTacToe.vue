<template>
  <table-component :table-data="tableData"></table-component>
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
  border: 3px solid black;
  width: 200px;
  height: 200px;
  text-align: center;
}
td:hover {
  background: #551155;
}
</style>