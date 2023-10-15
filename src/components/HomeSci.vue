<template>
  <v-container class="mt-10 flex-wrap" >
    <v-row>
      <v-col class="col-md-4" v-for="(card, index) in cards" :key="index" cols="12" md="4">
        <v-card
          class="mx-auto"
          max-width="344"
        >
        <v-img 
          :src="Image(card.locationPicture)" 
          height="200px"
        >
        </v-img>
        <v-card-title
          class="text-center d-flex justify-center align-center "
        >
          {{ card.locationName }}
        </v-card-title>
        <v-card-subtitle
        >
          {{ card.locationDescription }}
        </v-card-subtitle>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>


<script>
export default {
  data() {
    return {
      cards: [],
    };
  },
  methods: {
    async locationData() {
      try {
        const response = await this.axios.get("http://localhost:9000/location");
        this.cards = response.data;
      } catch (error) {
        console.error("Error fetching location data:", error);
      }
    },Image(locationPicture) {
      return `data:image/jpeg;base64,${locationPicture}`;
    },

  },
  created() {
    this.locationData();
  },

};
</script>
