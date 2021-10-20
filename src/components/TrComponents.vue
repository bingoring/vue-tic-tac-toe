<template>
    <tr>
        <td-component v-for="(cellData, index) in rowData" :cell-data="cellData" :cell-index="index" :row-index="rowIndex" :key="index"></td-component>        
    </tr>
</template>

<script>
import TdComponent from './TdComponent';
export default {
    props: {
        rowData: Array,
        rowIndex: Number,
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