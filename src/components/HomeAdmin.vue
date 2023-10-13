<template>
  <v-row>
    <v-col cols="3">
      <v-card
        class="mx-auto"
        max-width="344"
        @click="goToEditDelete()" 
      >
        <v-img 
          src="https://ced.sci.psu.ac.th/img/ced1.JPG"
          height="200px"
        ></v-img>

        <v-card-title>
          คณะวิทยาศาสตร์
        </v-card-title>

        <v-card-subtitle>
          มหาวิทยาลัยสงขลานครินทร์ วิทยาเขตหาดใหญ่
        </v-card-subtitle>

        <!-- <v-card-actions>
          <v-btn
            color="orange lighten-2"
            text
          >
            Explore
          </v-btn>

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
        </v-expand-transition> -->
      </v-card>
    </v-col>
 
    <v-col cols="3">
      <v-card
        class="mx-auto"
        max-width="344"
      >
        <v-img 
          src="https://shorturl.asia/u8Cty"
          height="200px"
        ></v-img>

        <v-card-title>
          คณะวิศวกรรมศาสตร์
        </v-card-title>

        <v-card-subtitle>
          มหาวิทยาลัยสงขลานครินทร์ วิทยาเขตหาดใหญ่
        </v-card-subtitle>

        <!-- <v-card-actions>
          <v-btn
            color="orange lighten-2"
            text
          >
            Explore
          </v-btn>

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
        </v-expand-transition> -->
      </v-card>
    </v-col> 

    <v-col cols="3">
      <v-card
        class="mx-auto"
        max-width="344"
      >
        <v-img 
          src="https://f.ptcdn.info/867/048/000/okei8m6mdpAXohH5Cdh-o.jpg"
          height="200px"
        ></v-img>

        <v-card-title>
          คณะนิติศาสตร์
        </v-card-title>

        <v-card-subtitle>
          มหาวิทยาลัยสงขลานครินทร์ วิทยาเขตหาดใหญ่
        </v-card-subtitle>

        <!-- <v-card-actions>
          <v-btn
            color="orange lighten-2"
            text
          >
            Explore
          </v-btn>

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
        </v-expand-transition> -->
      </v-card>
    </v-col>




    <v-col cols="3">
      <v-card
        class="mx-auto"
        max-width="344"
        
      >

        <v-img 
          src="https://www.fms.psu.ac.th/wp-content/uploads/2020/04/vision.jpg"
          height="200px"
        ></v-img>

        <v-card-title>
          คณะวิทยาการจัดการ
        </v-card-title>

        <v-card-subtitle>
          มหาวิทยาลัยสงขลานครินทร์ วิทยาเขตหาดใหญ่
        </v-card-subtitle>

        <!-- <v-card-actions>
          <v-btn
            color="orange lighten-2"
            text
          >
            Explore
          </v-btn>

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
        </v-expand-transition> -->
      </v-card>
    </v-col>
  </v-row>
</template>





<script>
export default {
  data: () => ({
    show: false,
  }),
  methods: {
      goToEditDelete() {
      this.$router.push('/EditDelete') // นำทางไปยังหน้า EditDelete
    }
  }
}
</script>