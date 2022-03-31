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
    <v-toolbar-title>Rad oder Regen?</v-toolbar-title>   

      <v-spacer></v-spacer>
      <v-icon color="yellow" :v-if="lightbulb()">mdi-lightbulb-on</v-icon>
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
  }),
  methods:{
    currentEvent(value){
      console.log(value);
      this.weatherData=value;
      this.showDummenSpruch=true;

    },
    hourSelected(value){
      this.currentlySelectedHour=value;
    },
    lightbulb(){
      return true;
    }
  }
};
</script>
<style>#app {
  background: url('./assets/rad_oder_regen_logo.png') no-repeat center center fixed !important;
  background-size: cover;
}</style>