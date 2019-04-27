<template>
    <button @click='checkFlag(flagIndex,gridSize)'>
        check
    </button>
</template>

<script>
import Flags from '../flags/flags.json';

export default {
    name: 'check-flag',
    data: function(){
        return{
            flags: Flags
        }
    },
    props: [
        'flagIndex',
        'gridSize',
        'points'
    ],
    methods: {
        checkFlag(findex, gsize){
            this.$emit('checkFlag',findex, gsize);
        }
    }
}
</script>

<style scoped>
    button{
        margin-top: 16px;
        font-size: 16px;
        cursor: pointer;
        outline: none;
    }
</style>
