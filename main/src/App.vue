<template>

  <v-app>

    <v-app-bar
      app
      color="#35682d"
      dark
    >

    <v-img
    max-height="60"
    max-width="60"
    src="./assets/zyro-image.png">

    </v-img>
    <v-toolbar-title>Rad oder Regen</v-toolbar-title>   

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-main>
      <ButtonsMain @current-event="currentEvent" @hour-selected="hourSelected" :weatherData="weatherData"></ButtonsMain>
      <HelloWorld :showDummenSpruch="showDummenSpruch" :currentlySelectedHour="currentlySelectedHour" />
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
    }
  }
};
</script>
