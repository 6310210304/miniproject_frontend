<template>
  <v-card
    class="mx-auto"
    max-width="344"
  >
    <v-img
      src="https://ced.sci.psu.ac.th/img/ced1.JPG"
      height="200px"
    ></v-img>

    <v-card-title>
      คณะวิทยาศาสตร์
    </v-card-title>

    <v-card-subtitle>
      1,000 miles of wonder
    </v-card-subtitle>

    <v-card-actions>
      <!-- <v-btn
        color="orange lighten-2"
        text
      >
        Explore
      </v-btn> -->

      <v-spacer></v-spacer>

      <v-btn
        icon
        @click="show = !show"
      >
        <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
      </v-btn>
    </v-card-actions>

    <v-expand-transition>
      <div v-show="show">
        <v-divider></v-divider>

        <v-card-text>
          I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for sleeping, soldier, not with all the bed making you'll be doing. Then we'll go with that data file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to escape.
        </v-card-text>
      </div>
    </v-expand-transition>


    <v-img
      src="data:image/jpeg;base64,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"
      height="200px"
    ></v-img>

    <v-card-title>
      คณะศิลปศาสตร์
    </v-card-title>

    <v-card-subtitle>
      1,000 miles of wonder
    </v-card-subtitle>

    <v-card-actions>
      <!-- <v-btn
        color="orange lighten-2"
        text
      >
        Explore
      </v-btn> -->

      <v-spacer></v-spacer>

      <v-btn
        icon
        @click="show = !show"
      >
        <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
      </v-btn>
    </v-card-actions>

    <v-expand-transition>
      <div v-show="show">
        <v-divider></v-divider>

        <v-card-text>
          I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for sleeping, soldier, not with all the bed making you'll be doing. Then we'll go with that data file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to escape.
        </v-card-text>
      </div>
    </v-expand-transition>


    <v-img
      src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
      height="200px"
    ></v-img>

    <v-card-title>
      Top western road trips
    </v-card-title>

    <v-card-subtitle>
      1,000 miles of wonder
    </v-card-subtitle>

    <v-card-actions>
      <!-- <v-btn
        color="orange lighten-2"
        text
      >
        Explore
      </v-btn> -->

      <v-spacer></v-spacer>

      <v-btn
        icon
        @click="show = !show"
      >
        <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
      </v-btn>
    </v-card-actions>

    <v-expand-transition>
      <div v-show="show">
        <v-divider></v-divider>

        <v-card-text>
          I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for sleeping, soldier, not with all the bed making you'll be doing. Then we'll go with that data file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to escape.
        </v-card-text>
      </div>
    </v-expand-transition>


    <v-img
      src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
      height="200px"
    ></v-img>

    <v-card-title>
      Top western road trips
    </v-card-title>

    <v-card-subtitle>
      1,000 miles of wonder
    </v-card-subtitle>

    <v-card-actions>
      <!-- <v-btn
        color="orange lighten-2"
        text
      >
        Explore
      </v-btn> -->

      <v-spacer></v-spacer>

      <v-btn
        icon
        @click="show = !show"
      >
        <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
      </v-btn>
    </v-card-actions>

    <v-expand-transition>
      <div v-show="show">
        <v-divider></v-divider>

        <v-card-text>
          I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for sleeping, soldier, not with all the bed making you'll be doing. Then we'll go with that data file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to escape.
        </v-card-text>
      </div>
    </v-expand-transition>
  </v-card>
</template>




<script>
export default {
  data: () => ({
    show: false,
  }),
  methods: {
      Homepage () {
          if (this.$refs.form.validate()) {
              localStorage.setItem('username', this.name)
          } 
      }
  }
}
</script>










