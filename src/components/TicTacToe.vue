<template>
<div>
  <div>{{turn}}님의 턴입니다.</div>
  <table-component :table-data="tableData"></table-component>
  <div v-if="winner">{{winner}}님의 승리!</div>
</div>
  
</template>

<script>
import Vue from 'vue';
import EventBus from './EventBus.js';
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
      turn: 'O',
      winner: '',
    };
  },
  methods:{
    onChangeData(){
      //Vue.set(this.tableData[1], 0, 'x');
      this.$set(this.table[i], 0, 'X');
    },
    onClickTd(rowIndex, cellIndex){
      this.$set(this.tableData[rowIndex], [cellIndex], this.turn);

      let win = false;
      if(this.tableData[rowIndex][0] === this.turn && this.tableData[rowIndex][1] === this.turn && this.tableData[rowIndex][2] == this.turn) win = true;
      if(this.tableData[0][cellIndex] === this.turn && this.tableData[1][cellIndex] === this.turn && this.tableData[2][cellIndex] === this.turn) win = true;
      if(this.tableData[0][0] === this.turn && this.tableData[1][1] === this.turn && this.tableData[2][2] === this.turn) win = true;
      if(this.tableData[0][2] === this.turn && this.tableData[1][1] === this.turn && this.tableData[2][0] === this.turn) win = true;
        
      if(win){
        this.winner = this.turn;
        this.turn = 'O';
        this.tableData =[
          ['','',''],
          ['','',''],
          ['','','']
        ]
      }else{
        let all = true;
          this.tableData.forEach((row) => {
            row.forEach((cell) => {                
              if(!cell){
                all = false;
                }
              });
          });
          if(all){
              //무승부/
              this.winner = '';
              this.turn = 'O';
              this.tableData = [
                  ['','',''],
                  ['','',''],
                  ['','',''],
              ]
          } else{
              this.turn = this.turn === 'O' ? 'X' : 'O';
          }
        }
    }
  },
  created(){
    EventBus.$on('clickTd', this.onClickTd);
    EventBus.$on('clickTr', this.onClickTr);
    EventBus.$on('clickTable', this.onClickTable);
  }
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
  transition-duration: 3ms;
}
td:hover {
  transition-duration: 20ms;

  background: #551155;
}
</style>