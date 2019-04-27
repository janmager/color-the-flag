<template>
    <div>
        <div v-bind:class="{grid1:gridStyle1,grid2:gridStyle2}">
            <div 
                class="grid-item"
                v-for='(block, index) in blocks'
                :key='index'
                :id="'p'+index"
                :style="'background:'+block.color"
                @mouseover.ctrl='setBlockColor(index)'></div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'color-grid',
    props: [
        'color',
        'flags',
        'flagIndex',
        'gridSize'
    ],
    data: function(){
        return{
            blocks: [],
            gridStyle1: false,
            gridStyle2: true
        }
    },
    methods: {
        initGrid(){
            for(let i = 0;i<this.gridSize; i++){
                this.blocks.push({
                    color: '#F4F4F4'
                })
            }
        },
        setBlockColor(index){
            this.blocks[index].color = this.color;
        }
    },
    mounted(){
        console.log('gs='+this.gridSize);
        
        if(this.gridSize==150){
            this.gridStyle2 = false;
            this.gridStyle1 = true;
        }
        else if(this.gridSize==128){
            this.gridStyle1 = false;
            this.gridStyle2 = true;
        }
        this.initGrid();
    }
}
</script>

<style scoped>
    .grid1{
        display: grid;
        grid-template-columns: repeat(15, 1fr);
        grid-template-rows: repeat(10, 1fr);
        width: 480px;
        height: 320px;
        margin: 0 auto;
    }
    .grid2{
        display: grid;
        grid-template-columns: repeat(14, 1fr);
        grid-template-rows: repeat(9, 1fr);
        width: 448px;
        height: 288px;
        margin: 0 auto;
    }
    .grid-item{
        border: 1px dashed #CCC;
    }
</style>
