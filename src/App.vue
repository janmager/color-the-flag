<template>
  <div id="app">
    <Header :color='color' />
    <p>Choose the color you want to color.</p>
    <ColorPicker :colors='colors' @setColor='setColor' />
    <p>Hold CTRL button and move mouse to color the flag.</p>
    <ColorGrid :color='color' :flags='flags' />
  </div>
</template>

<script>
import Header from '@/components/Header';
import ColorPicker from '@/components/ColorPicker';
import ColorGrid from '@/components/ColorGrid';
import Flags from './flags/flags.json';

export default {
  name: 'app',
  components: {
    Header,
    ColorPicker,
    ColorGrid
  },
  data: function(){
    return{
      flags: Flags,
      colorsTemp: [],
      colors: [],
      color: '#FFF'
    }
  },
  methods: {
    setColor(color){
      this.color = color;
    },
    checkFlag(){
      alert('checking...');
    }
  },
  created(){
    var numbers = [0, 1, 2, 3, 4];

    function randColor(){
      return '#'+Math.floor(Math.random()*16777215).toString(16);
    }
    
    this.colorsTemp.push(this.flags.Flags[0].colorToPick[0].color);
    this.colorsTemp.push(this.flags.Flags[0].colorToPick[1].color);
    for(var i=0;i<3;i++){
      var randed = randColor();
      this.colorsTemp.push(randed);
    }

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
