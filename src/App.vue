<template>
  <div id="app">
    <Header :color='color' />
    <RandomedFlag :flagIndex='flagIndex' />
    <p>Choose the color you want to color.</p>
    <ColorPicker :colors='colors' @setColor='setColor' />
    <p>Hold CTRL button and move mouse to color the flag.</p>
    <ColorGrid :color='color' :flags='flags' :flagIndex='flagIndex' :gridSize='gridSize' />
    <CheckFlag :flagIndex='flagIndex' :gridSize='gridSize' @checkFlag='checkFlag' :points='points' />
  </div>
</template>

<script>
import Header from '@/components/Header';
import ColorPicker from '@/components/ColorPicker';
import ColorGrid from '@/components/ColorGrid';
import Flags from './flags/flags.json';
import RandomedFlag from './components/RandomedFlag';
import CheckFlag from './components/CheckFlag';
import { log } from 'util';

export default {
  name: 'app',
  components: {
    Header,
    ColorPicker,
    ColorGrid,
    RandomedFlag,
    CheckFlag
  },
  data: function(){
    return{
      flags: Flags,
      colorsTemp: [],
      colors: [],
      color: '#FFF',
      flagIndex: null,
      gridSize: null,
      points: 0
    }
  },
  methods: {
    setColor(color){
      this.color = color;
    },
    checkFlag(findex,gsize){
      var pointsVar = 0;
      var hexDigits = new Array("0","1","2","3","4","5","6","7","8","9","a","b","c","d","e","f"); 

      function rgb2hex(rgb) {
        rgb = rgb.match(/^rgb\((\d+),\s*(\d+),\s*(\d+)\)$/);
        return "#" + hex(rgb[1]) + hex(rgb[2]) + hex(rgb[3]);
      }

      function hex(x) {
        return isNaN(x) ? "00" : hexDigits[(x - x % 16) / 16] + hexDigits[x % 16];
      }
      console.log('gsize='+gsize);
      
      for(let i = 0;i<gsize;i++){
        let cell = document.getElementById('p'+i);
        let cellColor = cell.style.backgroundColor;
        cellColor = rgb2hex(cellColor);
        let correctColor = this.flags.Flags[findex].colors[i].color;                
        if(cellColor == correctColor) pointsVar++;
      }
      this.points = pointsVar;
      console.log('pkt: '+this.points);
      console.log('next one, but now not: '+this.flags.Flags[findex].name);
      let con = confirm('Zdobyte punkty: '+this.points+'/'+this.gridSize+' - '+((this.points*100)/this.gridSize).toFixed(2)+'%');
      if(con){ console.log('start new game...') };
    },
    newGame(){
      var numbers = [0, 1, 2, 3, 4];

      // random flag index
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
      
      // show colors in log
      // for(var i=0;i<5;i++){
      //   console.log(this.colors[i]);
      // }
    }
  },
  mounted(){
    this.newGame();
  },
  beforeMount(){
    var len = this.flags.Flags.length;
    this.flagIndex = Math.floor((Math.random()*len));
    
    // type of flag (proportion)
    if(this.flags.Flags[this.flagIndex].type==1) this.gridSize = 150;
    else if(this.flags.Flags[this.flagIndex].type==2) this.gridSize = 126;
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
