<template>
    <tr>
        <td-component v-for="(cellData, index) in rowData" :cell-data="cellData" :cell-index="index" :row-index="rowIndex" :key="index" :turn="turn"></td-component>        
    </tr>
</template>

<script>
import TdComponent from './TdComponent';
export default {
    props: {
        rowData: Array,
        rowIndex: Number,
        turn: String,
    },
    data() {
        return{
            parent: '애비',
        };
    },
    components: {
        TdComponent,
    },
}
</script>