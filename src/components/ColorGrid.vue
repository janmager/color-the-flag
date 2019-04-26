<template>
    <div>
        <div class="grid">
            <div 
                class="grid-item"
                v-for='(block, index) in blocks'
                :key='index'
                :id="'p'+index"
                :style="'background:'+block.color"
                @mouseover.ctrl='setBlockColor(index)'></div>
        </div>
        <button @click='checkFlag'>
            check
        </button>
    </div>
</template>

<script>
export default {
    name: 'color-grid',
    props: [
        'color',
        'flags',
        'flagIndex'
    ],
    data: function(){
        return{
            blocks: [],
            gridSize: 150
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
        },
        checkFlag(){
            var points = 0;
            var hexDigits = new Array("0","1","2","3","4","5","6","7","8","9","a","b","c","d","e","f"); 

            function rgb2hex(rgb) {
                rgb = rgb.match(/^rgb\((\d+),\s*(\d+),\s*(\d+)\)$/);
                return "#" + hex(rgb[1]) + hex(rgb[2]) + hex(rgb[3]);
            }

            function hex(x) {
                return isNaN(x) ? "00" : hexDigits[(x - x % 16) / 16] + hexDigits[x % 16];
            }

            for(let i = 0;i<150;i++){
                let cell = document.getElementById('p'+i);
                let cellColor = cell.style.backgroundColor;
                cellColor = rgb2hex(cellColor);
                let correctColor = this.flags.Flags[this.flagIndex].colors[i].color;
                
                if(cellColor == correctColor) points++;
            }
            
            console.log('Zdobyte punkty: '+points+'/'+this.gridSize);
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
        grid-template-columns: repeat(15, 1fr);
        grid-template-rows: repeat(10, 1fr);
        width: 480px;
        height: 320px;
        margin: 0 auto;
    }
    .grid-item{
        border: 1px dashed #CCC;
    }
</style>
