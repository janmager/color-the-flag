<template>
  <div id="app">
    <Header :color='color' />
    <RandomedFlag :flagIndex='flagIndex' />
    <p>Choose the color you want to color.</p>
    <ColorPicker :colors='colors' @setColor='setColor' />
    <p>Hold CTRL button and move mouse to color the flag.</p>
    <ColorGrid :color='color' :flags='flags' :flagIndex='flagIndex' />
  </div>
</template>

<script>
import Header from '@/components/Header';
import ColorPicker from '@/components/ColorPicker';
import ColorGrid from '@/components/ColorGrid';
import Flags from './flags/flags.json';
import RandomedFlag from './components/RandomedFlag';
import { log } from 'util';

export default {
  name: 'app',
  components: {
    Header,
    ColorPicker,
    ColorGrid,
    RandomedFlag
  },
  data: function(){
    return{
      flags: Flags,
      colorsTemp: [],
      colors: [],
      color: '#FFF',
      flagIndex: 1
    }
  },
  methods: {
    setColor(color){
      this.color = color;
    }
  },
  created(){
    var numbers = [0, 1, 2, 3, 4];
    
    // random flag index
    var len = this.flags.Flags.length;
    this.flagIndex = Math.floor((Math.random()*len));
    var colorLen = this.flags.Flags[this.flagIndex].colorToPick.length;
    var rest = 0;

    // pushing to array must have colors
    for(var i=0;i<colorLen;i++){
      if((i+1)==colorLen) rest = (5-(i+1));
      this.colorsTemp.push(this.flags.Flags[this.flagIndex].colorToPick[i].color);
    }

    // pushing to array randomed additional colors
    for(var i=0;i<rest;i++){
      var randed = randColor();
      this.colorsTemp.push(randed);
    }

    // generating random color
    function randColor(){
      return '#'+Math.floor(Math.random()*16777215).toString(16);
    }

    // mixing colors
    function shuffle(o) {
      for(var j, x, i = o.length; i; j = parseInt(Math.random() * i), x = o[--i], o[i] = o[j], o[j] = x);
      return o;
    }
    var rand = shuffle(numbers);  
    for(var i=0;i<5;i++){
      this.colors.push(this.colorsTemp[rand[i]]);
    }
  }
}
</script>

<style>
body{
  margin: 0;
  padding: 0;
  background: #F3F3F3;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
