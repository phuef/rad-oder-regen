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
      <ButtonsMain @current-event="currentEvent" :weatherData="weatherData"></ButtonsMain>
      <HelloWorld/>
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
  }),
  methods:{
    currentEvent(value){
      console.log(value);
      this.weatherData=value;

    }
  }
};
</script>
