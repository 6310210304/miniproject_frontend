<template>
  <v-app style="color: #33CCCC" >
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <!-- <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src=""
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Recommended food center Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src=""
          width="100"
        /> -->
        
          
        <v-btn
          text
          @click="goToHome()"
        >
          Recommended food center
        </v-btn>
      </div>

      <v-spacer></v-spacer>

      <!-- <v-btn
        text
        @click="goToManage()"
      >
        หน้าจัดการข้อมูล
      </v-btn> -->

      <v-btn
        text
        @click="gotoHomepage()"
      >
        หน้าแรก
      </v-btn>


      <v-btn
        text
        @click="goToLogin()"
      >
        เข้าสู่ระบบ
      </v-btn>

      <!-- <v-btn
        text
        @click="goToRegister()"
      >
        สมัครสมาชิก
      </v-btn> -->


    </v-app-bar>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
  }),
  methods: {
    goToHome() {
      this.$router.push('/')
    },
    goToLogin() {
      this.$router.push('/login')
    },
    goToManage() {
      this.$router.push('/manageTable')
      // this.$router.push({path: })
    },
    goToRegister() {
      this.$router.push('/Register')
    },
    gotoHomepage() {
      this.$router.push('/Homepage')
    }
    ,
    gotoAdd() {
      this.$router.push('/add')
    }
  }
}
</script>