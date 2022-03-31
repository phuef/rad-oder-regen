<template>
  <v-container v-if="currentlySelectedHour">
   <v-flex>
     <v-card class="mx-auto"
    :color="getColor()"
    dark
    max-width="400"
>
  <v-card-text class="text-h5 font-weight-bold">
      "{{dummerSpruchGenerator()}}"
    </v-card-text>
    <v-card-actions>

      <v-list-item class="grow">

        <v-row
          align="center"
        >
        <v-icon class="mr-1">
            mdi-thermometer
          </v-icon>
          <span class="subheading mr-2">{{computeWeatherData().temp}}°C</span>
          <v-icon class="mr-1">
            mdi-weather-rainy
          </v-icon>
          <span class="subheading mr-2">{{computeWeatherData().precip}}</span>
          <span class="mr-1">·</span>
          <v-icon class="mr-1">
            mdi-water-percent
          </v-icon>
          <span class="subheading">{{computeWeatherData().precipprob}}</span>
        </v-row>
      </v-list-item>

      
    </v-card-actions>
   </v-card>
   </v-flex>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',
    props: {
      showDummenSpruch:{default: false},
      currentlySelectedHour:{default:false},
      weatherData:{default: false},
    },

    data: () => ({
      dummeSpruecheRegenGroeßer5: [ 
        "Fahr lieber mit dem Boot",
        "Du sparst dir die Dusche",
      ],
      dummeSpruecheRegenKleiner1:[
        "Bist du aus Zucker",
        "Da hat wohl jemand seinen Teller gestern nicht aufgegessen"
      ],
      dummeSpruecheRegen1bis5:[
        "Es geht im Leben nicht darum zu warten bis das Unwetter vorbei ist sondern zu lernen im Regen zu tanzen",
        "Wenn man die Augen zu macht klingt der Regen nach Applaus",
        "Auch Regen ist schön, wenn man die Sonne im Herzen hat",
        "Es gibt kein schlechtes Wetter, nur schlechte Frisuren",
      ],
      dummeSpruecheSchnee: [
        "Schnee ist auch nur Konfetti das aus den Wolken fällt",
        "Wo nicht glatt ist, kannst du fahren",
        "Du kannst mit dem Schlitten fahren"
      ],
      dummeSpruecheGutesWetter: [
        "Fahr doch",
        "Besser wirds nicht",
        "Genieß die frische Luft"
      ],
    }),
    methods:{
      computeWeatherData(){
        console.log(this.weatherData);
        var current=this.weatherData.days[0].hours[this.currentlySelectedHour];
        return current;
      },
      getColor(){
        if (this.computeWeatherData().preciptype){
          if(this.computeWeatherData().preciptype[0]=="rain")
          {
            return '#63b8ff'
          }
          else if(this.computeWeatherData().preciptype[0]=="snow"){
            return '#8c8c8c'
          }
        }
        else{return '#ffc125'}
        /*switch (this.computeWeatherData().preciptype){
          case ["snow"]: return '#8c8c8c';
          case null: return '#ffc125';
          case ["rain"]: return '#63b8ff';
        }*/
      },
      dummerSpruchGenerator(){
        var val= this.computeWeatherData().precip;
        if(this.computeWeatherData()?.preciptype[0]=="snow"){
          return this.randomSpruch(this.dummeSpruecheSchnee);
        }
        else if(val== 0.0){return this.randomSpruch(this.dummeSpruecheGutesWetter);}
        else if(val<1){return this.randomSpruch(this.dummeSpruecheRegenKleiner1);}
        else if(val<=5){return this.randomSpruch(this.dummeSpruecheRegen1bis5);}
        else if(val>5){return this.randomSpruch(this.dummeSpruecheRegenGroeßer5);}
      },
      randomSpruch(arr){
        const idx = Math.floor(Math.random() * arr.length);
        return arr[idx];
      }
    },
  }
</script>
