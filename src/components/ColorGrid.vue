<template>
    <div class="grid">
        <div 
            class="grid-item"
            v-for='(block, index) in blocks'
            :key='index'
            :style="'background:'+block.color"
            @click='setBlockColor(index)'></div>
    </div>
</template>

<script>
export default {
    name: 'color-grid',
    props: ['color'],
    data: function(){
        return{
            blocks: [],
            gridSize: 100
        }
    },
    methods: {
        initGrid(){
            for(let i = 0;i<this.gridSize; i++){
                this.blocks.push({
                    color: '#FFF'
                })
            }
        },
        setBlockColor(index){
            this.blocks[index].color = this.color;
        }
    },
    created(){
        this.initGrid();
    }
}
</script>

<style scoped>
    .grid{
        display: grid;
        grid-template-columns: repeat(10, 1fr);
        grid-template-rows: repeat(10, 1fr);
        width: 320px;
        height: 320px;
        margin: 0 auto;
    }
    .grid-item{
        border: 1px dashed #CCC;
    }
</style>
