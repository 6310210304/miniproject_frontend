<template>
  <div>
    <BarAdmin />
    <v-data-table :headers="headers" :items="reserveItem" class="elevation-1">
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>จัดการข้อมูล</v-toolbar-title>
          <v-divider class="mx-4" inset vertical></v-divider>
          <v-spacer></v-spacer>
        </v-toolbar>
      </template>

      <template v-slot:[`item.actions`]="{ item }">
        <v-btn small outlined @click="deleteItem(item)" color="red" class="ml-2">
          <v-icon>mdi-delete</v-icon>
        </v-btn>
      </template>
    </v-data-table>
    <v-dialog v-model="dialogCreate" max-width="500px"></v-dialog>

    <!-- ลบข้อมูล -->
    <v-dialog v-model="dialogDelete" max-width="500px">
      <v-card>
        <v-card-title class="text-h5">ตุณต้องการลบข้อมูลนี้ในตารางใช่ หรือ ไม่?</v-card-title>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="closeDelete">ยกเลิก</v-btn>
          <v-btn color="blue darken-1" text @click="deleteItemConfirm">ตกลง</v-btn>
          <v-spacer></v-spacer>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
  <script>
import BarAdmin from "@/components/BarAdmin.vue";

export default {
  data: () => ({
    reserveId: "",
    reserveDate: "",
    userId: "",
    areaId: "",
    dialogCreate: false,
    dialogDelete: false,
    headers: [
      {
        text: "ไอดี",
        align: "start",
        sortable: false,
        value: "user.userId"
      },

      { text: "วันที่จอง", value: "reserveDate" },
      { text: "พื้นที่จอง", value: "area.areaName" },
      { text: "จัดการ", value: "actions", sortable: false }
    ],
    reserveItem: [],
    editedIndex: -1,
    editedItem: {
      reserveId: "",
      reserveDate: "",
      userId: "",
      areaId: ""
    },
    defaultItem: {
      reserveId: "",
      reserveDate: "",
      userId: "",
      areaId: ""
    },
    formTitle: "",
    idreserve: "",
    idforDelete: ""
  }),

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    }
  },

  created() {
    this.initialize();
  },
  components: {
    BarAdmin
  },

  methods: {
    async initialize() {
      this.reserveItem = [];
      try {
        var data = await this.axios.get("http://localhost:8000/reserve");
        console.log("data reserve ====>", data);
        this.reserveItem = data.data;
        console.log(reserveItem);
      } catch (error) {}
    },

    deleteItem(item) {
      this.idForDelete = item.reserveId;
      this.dialogDelete = true;
    },

    async deleteItemConfirm() {

      try {
        var response = await this.axios.delete("http://localhost:8000/reserve/" + this.idForDelete);
        this.initialize();
      } catch (error) {
        console.log(error.message);
      }
      this.closeDelete();
    },

    close() {
  this.dialogCreate = false;
  this.editedItem = {};
  this.editedIndex = -1;
  this.defaultItem = {
    reserveId: "",
    reserveDate: "",
    userId: "",
    areaId: ""
  };
},

    closeDelete() {
      this.dialogDelete = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
this.editedIndex = -1;
      });
    }
  }
};
</script>
    
<style>

</style>