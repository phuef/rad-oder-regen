<template>

  <v-app background-image="./assets/Backgroundlogo.png"
          >

    <v-app-bar
      app
      color="#35682d"
      dark
    >

    <v-img
    max-height="60"
    max-width="60"
    src="./assets/rad_oder_regen_logo.png">

    </v-img>
    <v-spacer></v-spacer>
    <v-toolbar-title :style="{ color: getRadColor()}"> Rad  </v-toolbar-title> 
        <v-spacer></v-spacer>

    <v-toolbar-title> oder  </v-toolbar-title> 
        <v-spacer></v-spacer>
 
    <v-toolbar-title :style="{ color: getRegenColor(), 'text-decoration': underlineRegen()}"> {{isRegen()}}?</v-toolbar-title>    

      <v-spacer></v-spacer>
      <v-icon color="#ffc125"  v-if="lightbulb">mdi-lightbulb-on</v-icon>
     
    </v-app-bar>

    <v-main>
      <HelloWorld :showDummenSpruch="showDummenSpruch" :currentlySelectedHour="currentlySelectedHour" :weatherData="weatherData"/>
      <ButtonsMain @current-event="currentEvent" @hour-selected="hourSelected" :weatherData="weatherData"></ButtonsMain>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import ButtonsMain from './components/ButtonsMain';

export default {
  name: 'App',

  components: {
    HelloWorld,
    ButtonsMain,
  },

  data: () => ({
    weatherData:null,
    showDummenSpruch:false,
    currentlySelectedHour:null,
    sunrise:'00:00',
    sunset:'23:59',
  }),
  computed:{
    lightbulb(){
      return (this.currentlySelectedHour<=this.sunrise|| this.currentlySelectedHour>=this.sunset) ? true : false;
    },
  },
  mounted(){
    if(this.weatherData){
      this.sunrise= this.weatherData.days[0].sunrise.substring(0,2);
      this.sunset= this.weatherData.days[0].sunset.substring(0,2);
    }
  },
  methods:{
    currentEvent(value){
      console.log(value);
      this.weatherData=value;
      this.sunrise= this.weatherData.days[0].sunrise.substring(0,2);
      this.sunset= this.weatherData.days[0].sunset.substring(0,2);
      this.showDummenSpruch=true;

    },
    getRegenColor(){
      if (this.weatherData?.days[0].hours[this.currentlySelectedHour].preciptype[0]== 'rain'){
      return '#63b8ff'}
      else if( 
      this.weatherData?.days[0].hours[this.currentlySelectedHour].preciptype[0]== 'snow'){
        return 'grey'
      }
      return 'white';
    },
    getRadColor(){
      if (this.weatherData?.days[0].hours[this.currentlySelectedHour].preciptype[0]== 'snow'&& 
          this.weatherData?.days[0].hours[this.currentlySelectedHour].precip>0.2){
      return 'red'}
      else if (this.weatherData?.days[0].hours[this.currentlySelectedHour].preciptype[0]== 'snow'&& 
          this.weatherData?.days[0].hours[this.currentlySelectedHour].precip<=0.2){
      return '#ffc125'}
      else if(this.weatherData?.days[0].hours[this.currentlySelectedHour].preciptype[0]== 'rain' && 
        this.weatherData?.days[0].hours[this.currentlySelectedHour].precip>1){
          return '#ffc125'
        }
        else if(this.weatherData?.days[0].hours[this.currentlySelectedHour].precip>5){return 'red'}
      return '#ADFF00'
    },
    underlineRegen(){
      if (this.weatherData?.days[0].hours[this.currentlySelectedHour].preciptype[0]== 'rain'){
      return 'underline'}
      else if( 
      this.weatherData?.days[0].hours[this.currentlySelectedHour].preciptype[0]== 'snow'){
        return 'underline'
      }
      return 'line-through';
    },
    isRegen(){
      
      if(this.weatherData?.days[0].hours[this.currentlySelectedHour].preciptype[0]== 'snow'){
        return 'Schnee'
      }
      return 'Regen'
    },
    hourSelected(value){
      this.currentlySelectedHour=value;
    },}
};
</script>
<style>#app {
  background: url('./assets/rad_oder_regen_logo.png') no-repeat center center fixed !important;
  background-size: cover;
}</style>