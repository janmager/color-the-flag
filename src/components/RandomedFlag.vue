<template>
    <div>
       Draw flag: <span>{{this.flagIndexNew}}</span>
    </div> 
</template>

<script>
import Flags from '../flags/flags.json';

export default {
    name: 'randomed-flag',
    data: function(){
        return{
            flags: Flags,
            flagIndexNew: null
        }
    },
    props: [
        'flagIndex'
    ],
    created(){
        this.flagIndexNew = this.flags.Flags[this.flagIndex].name;
        // console.log(this.flags.Flags.length);
        
    }
}
</script>

<style scoped>
    div{
        margin-top: 16px;
    }
    span{
        font-weight: bold;
    }
</style>
