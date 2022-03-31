<template>
    <v-container>
          <v-card-title>Sollte ich heute mit dem Rad fahren?</v-card-title>
          <v-btn elevation="2" @click="showCurrentWeather()">jetzt</v-btn>
          <v-btn elevation="2" @click="showWeatherInAnHour()">in einer Stunde</v-btn>
          <v-row justify="space-around" v-if="andereZeit">
            <v-time-picker
              class="mt-4"
              format="24hr"
              no-title
              ref="picker"
              @click:hour="selectingHourIfUseHoursOnly"
            ></v-time-picker>
          </v-row>

  <v-card-title v-if="isWeatherData()">{{hours}} </v-card-title>

    </v-container>
</template>
<script>
  export default {
    name: 'ButtonsMain',

    props: {
      weatherData:null,
    },

    data: () => ({
      andereZeit:true,
      hours:0,
      dataResponse:{"test":"test"},
    }),
    methods:{
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
        return this.weatherData;
      },
      isAndereZeit(){
        if(this.andereZeit){
        this.andereZeit=!this.isAndereZeit;}
        else {this.andereZeit=true}
      },
      selectingHourIfUseHoursOnly() {
        this.$nextTick(() => {
          this.$refs.picker.selectingHour = true;
          this.hours=this.$refs.picker.inputHour;
          this.$emit('hours-selected', this.$refs.picker.inputHour)
        });
  }},
  created(){
    fetch("https://weather.visualcrossing.com/VisualCrossingWebServices/rest/services/timeline/m%C3%BCnster/2022-03-31/2022-03-31?unitGroup=metric&elements=datetime%2Ctemp%2Cprecip%2Cprecipprob%2Cprecipcover%2Cpreciptype&include=fcst%2Cstatsfcst%2Cdays%2Chours%2Ccurrent&key=EETCRGZNWWFRHX2FA59KZAZCB&contentType=json", {
        "method": "GET",
        "headers": {
        }
        })
        .then((response) => response.json())
          .then((responseJSON) => {
            // do stuff with responseJSON here...
            console.log(responseJSON);
            this.$emit('current-event', responseJSON)
            this.dataResponse=responseJSON;
          })
      /*.then(response => {
        console.log(response);
        this.$emit('current-event', response)
        this.dataResponse=response.JSON;
      })*/
      .catch(err => {
        console.error(err);
      });
      }
}
</script>

<style>

</style>
