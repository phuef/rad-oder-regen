<template>
    <v-container>
          <v-row justify="space-around" v-if="andereZeit">
            <v-time-picker
              v-model="time"
              class="mt-4"
              format="24hr"
              no-title
              ref="picker"
              @click:hour="selectingHourIfUseHoursOnly"
            ></v-time-picker>
          </v-row>
          <v-row justify="space-around" v-if="andereZeit">
              <v-btn rounded elevation="2" @click="showWeatherInAnHour()">in einer Stunde</v-btn>
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
      andereZeit:true,
      dataResponse:{"test":"test"},
      time:'18:00',
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
      showWeatherInAnHour(){
        var temp= this.time.substring(0,2);
        temp++;
        if (temp<10)
        {
          this.$emit('hour-selected', temp);
          temp='0' +temp
        }
        else {
          this.$emit('hour-selected', temp);
        }
        this.time= '' +temp +':00';
        


      },
      isAndereZeit(){
        if(this.andereZeit){
        this.andereZeit=!this.isAndereZeit;}
        else {this.andereZeit=true}
      },
      selectingHourIfUseHoursOnly() {
        this.$nextTick(() => {
          this.$refs.picker.selectingHour = true;
          this.$emit('hour-selected', this.$refs.picker.inputHour)
        });
  }},
  mounted(){
    const d = new Date();
    let hour = d.getHours();
    console.log(hour);
    this.time=''+hour +':00'
    this.$emit('hour-selected', hour);
  },
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
      .catch(err => {
        console.error(err);
      });
      }
}
</script>

