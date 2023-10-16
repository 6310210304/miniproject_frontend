<template>
  <v-container class="mt-10 flex-wrap" >
    <v-row>
      <v-col class="col-md-4" v-for="(card, index) in cards" :key="index" cols="12" md="3">
        <v-card
          class="mx-auto"
          max-width="344"
          @click="goToHomeSci()"
        >
        <v-img 
          :src="Image(card.facultyPicture)" 
          height="200px"
        >
        </v-img>
        <v-card-title 
          class="text-center d-flex justify-center align-center "
          style="height: 3rem"
        >
          {{ card.facultyName }}
        </v-card-title>
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
    async FacultyData() {
      try {
        const response = await this.axios.get("http://localhost:9000/faculty");
        this.cards = response.data;
      } catch (error) {
        console.error("Error fetching faculty data:", error);
      }
    },Image(facultyPicture) {
      return `data:image/jpeg;base64,${facultyPicture}`;
    },
    goToHomeSci() {
      this.$router.push("/HomeSci");
    },
  },
  created() {
    this.FacultyData();
  },

};
</script>
