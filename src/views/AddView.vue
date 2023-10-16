<template>
    <v-container>
        <v-row>
            <v-col cols="12">
                <Add/>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
export default {
    components: {
        Add: () => import('../components/Add.vue')
    },
    goToAdd() {
      this.$router.push('/add')
    }
    
}
</script>

<style>

</style>