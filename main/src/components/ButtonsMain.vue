<template>
    <v-container>
          <v-card-title>Sollte ich heute mit dem Rad fahren?</v-card-title>
          <v-btn elevation="2" @click="weatherRequestCurrent()">jetzt</v-btn>
          <v-btn elevation="2" @click="weatherRequest()">in einer Stunde</v-btn>
          <v-btn elevation="2" @click="weatherRequest(); isAndereZeit()">Um x Uhr</v-btn>
          <v-card-title v-if="isWeatherData()">{{showWeatherData()}}</v-card-title>

          <v-row justify="space-around" v-if="andereZeit">
    <v-time-picker
      v-model="timeStep"
      class="mt-4"
      format="24hr"
    ></v-time-picker>
  </v-row>

    </v-container>
</template>
<script>
  export default {
    name: 'ButtonsMain',

    props: {
      weatherData:null,
    },

    data: () => ({
      andereZeit:false,
    }),
    methods:{
      weatherRequestCurrent(){
fetch("https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/m%C3%BCnster/2022-03-31/2022-03-31?unitGroup=us&elements=datetime%2Ctemp%2Cprecip%2Cprecipprob%2Cprecipcover%2Cpreciptype&include=fcst%2Cstatsfcst%2Ccurrent&key=EETCRGZNWWFRHX2FA59KZAZCB&contentType=json", {
  "method": "GET",
  "headers": {
  }
  })
.then(response => {
  console.log(response);

  this.$emit('current-event', response)
})
.catch(err => {
  console.error(err);
});

      },
      weatherRequest(){
        fetch("https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/m%C3%BCnster/2022-03-31/2022-03-31?unitGroup=metric&elements=datetime%2Ctemp%2Cprecip%2Cprecipprob%2Cprecipcover%2Cpreciptype&include=fcst%2Cstatsfcst%2Cdays%2Chours%2Ccurrent&key=EETCRGZNWWFRHX2FA59KZAZCB&contentType=json", {
  "method": "GET",
  "headers": {
  }
  })
.then(response => {
  console.log(response);
})
.catch(err => {
  console.error(err);
});
      },
      isWeatherData(){
        if (this.weatherData==null){
          return false;
        }
        else{
          return true;
        }
      },
      showWeatherData(){
        console.log(this.weatherData);
        return this.weatherData.body;
      },
      isAndereZeit(){
        if(this.andereZeit){
        this.andereZeit=!this.isAndereZeit;}
        else {this.andereZeit=true}
      },
      selectingHourIfUseHoursOnly() {
    this.$nextTick(() => {
      this.$refs.picker.selectingHour = true;
    });
  },
}}
</script>
