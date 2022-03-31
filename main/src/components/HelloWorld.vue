<template>
  <v-container>
   <v-flex v-for="dummeSpruech in dummeSprueche" :key="dummeSpruech" >
     <v-card class="mx-auto"
    color="#26c6da"
    dark
    max-width="400"
>
  <v-card-text class="text-h5 font-weight-bold">
      "{{dummeSpruech}}"
    </v-card-text>
    <v-card-actions>
      
    </v-card-actions>
   </v-card>
   </v-flex>
  </v-container>
</template>

<script>
  export default {
    name: 'HelloWorld',

    data: () => ({
      dummeSprueche: [ 
        "Wenn man die Augen zu macht klingt der Regen nach Applaus",
        "Auch Regen ist schön, wenn man die Sonne im Herzen hat",
        "Es gibt kein schlechtes Wetter, nur schlechte Frisuren",
        "Da hat wohl jemand seinen Teller nicht aufgegessen gestern",
        "Bist du aus Zucker?",
      ],
    }),
  }
</script>
