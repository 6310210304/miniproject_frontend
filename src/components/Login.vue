<template>
    <v-card
    class="mx-auto"
    max-width="344"
    >
        <v-card-title class="mx-auto">เข้าสู่ระบบ</v-card-title>
        <v-card-text>
            <v-form
                ref="form"
                v-model="valid"
                lazy-validation
            >
            <v-text-field
                v-model="name"
                :counter="20"
                :rules="nameRules"
                label="ชื่อผู้ใช้"
                required
                outlined
            ></v-text-field>

            <v-text-field
                v-model="password"
                :rules="passwordRules"
                label="รหัสผ่าน"
                required
                outlined
            ></v-text-field>

            <v-checkbox
                v-model="checkbox"
                :rules="[v => !!v || 'You must agree to continue!']"
                label="Do you agree?"
                required
            ></v-checkbox>

            <v-btn
                :disabled="!valid"
                color="success"
                class="mr-4"
                block
                @click="goToHomeAdmin()" 
            >
                เข้าสู่ระบบ
            </v-btn>
            </v-form>
        </v-card-text>
    </v-card>
</template>

<script>
export default {
    data: () => ({
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'กรุณากรอกชื่อผู้ใช้งาน',
        v => (v && v.length <= 20) || 'กรุณากรอกชื่อผู้ใช้งานห้ามเกิน 20 ตัวอักษร',
      ],
      password: '',
      passwordRules: [
        v => !!v || 'กรุณากรอกรหัสผ่าน',
      ]
    }),
    methods: {
        goToHomeAdmin() {
            if (this.$refs.form.validate()) {
            localStorage.setItem('username', this.name)
            this.$router.push('/HomeAdmin') // นำทางไปยังหน้า HomeAdmin
            }
        }
    }
}
</script>

<style>

</style>


