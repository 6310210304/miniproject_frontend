<template>
  <div>
    <v-data-table :headers="headers" :items="desserts" class="elevation-1">
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>จัดการข้อมูล</v-toolbar-title>
          <v-divider class="mx-4" inset vertical></v-divider>
          <v-spacer></v-spacer>
          <v-dialog v-model="dialog" max-width="500px">
            <template v-slot:activator="{ on, attrs }">
              <v-btn color="primary" dark class="mb-2" v-bind="attrs" v-on="on">
                เพิ่ม
              </v-btn>
            </template>
            <v-card>
              <v-card-title>
                <span class="text-h5">{{ formTitle }}</span>
              </v-card-title>

              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="1" sm="6" md="4">
                      <v-text-field
                        v-model="editedItem.name"
                        label="Name"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field
                        v-model="editedItem.picture"
                        label="Picture"
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" sm="6" md="4">
                      <v-text-field
                        v-model="editedItem.description"
                        label="Description"
                      ></v-text-field>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="red darken-1" text @click="close"> Cancel </v-btn>
                <v-btn color="blue darken-1" text @click="save"> Save </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
          <v-dialog v-model="dialogDelete" max-width="500px">
            <v-card>
              <v-card-title class="text-h5"
                >คุณแน่ใจหรือว่าต้องการลบรายการนี้?</v-card-title
              >
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="closeDelete"
                >ยกเลิก</v-btn
                >
                <v-btn color="red darken-1" text @click="deleteItemConfirm"
                  >ตกลง</v-btn
                >
                <v-spacer></v-spacer>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-toolbar>
      </template>
      <template v-slot:item.locationPicture="{ item }">
         <img  :src="'data:image/jpeg;base64,' + item.locationPicture" alt="Image" style="max-width: 200px" />
       </template>

      <template v-slot:item.actions="{ item }">
        <v-icon
          color="yellow darken-1"
          big
          class="mr-2"
          @click="editItem(item)"
        >
          mdi-pencil
        </v-icon>
        <v-icon color="red darken-1" big @click="deleteItem(item)">
          mdi-delete
        </v-icon>
      </template>
      <template v-slot:no-data>
        <v-btn color="primary" @click="initialize"> Reset </v-btn>
      </template>
    </v-data-table>
  </div>
</template>


<script>
import HomeSci from "@/components/HomeSci.vue";

export default {
  data: () => ({
    dialog: false,
    dialogDelete: false,
    headers: [
      {
        text: "ชื่อ",
        align: "start",
        sortable: false,
        value: "locationName",
      },
      {
        text: "รูปภาพ",
        sortable: false,
        value: "locationPicture",
        // เพิ่ม scopedSlots เพื่อแสดงรูปภาพ
      },
      {
        text: "คำอธิบาย",
        value: "locationDescription",
      },
      {
        text: "จัดการ",
        align: "start",
        sortable: false,
        value: "actions",
      },
    ],

    desserts: [],
    editedIndex: -1,
    editedItem: {
      name: "",
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0,
    },
    defaultItem: {
      name: "",
      calories: 0,
      fat: 0,
      carbs: 0,
      protein: 0,
    },
  }),
  scopedSlots: {
    picture: (item) => {
      return this.$createElement("img", {
        attrs: {
          src: item.picture, // ใช้ URL รูปภาพจากข้อมูล
          alt: item.name, // ใช้ชื่อเป็นคำอธิบายรูปภาพ
          style: "max-width: 100px;", // กำหนดขนาดสูงสุดของรูปภาพ
        },
      });
    },
  },

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New Item" : "Edit Item";
    },
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    },
  },

  created() {
    this.initialize();
  },

  methods: {
    async initialize() {
      this.desserts = [];
      try {
        var data = await this.axios.get("http://localhost:9000/location");
        console.log("data employee ====>", data);
        this.desserts = data.data;
      } catch (error) {}
    },

    computed: {
      formTitle() {
        return this.editedIndex === -1 ? "New Item" : "Edit Item";
      },
    },

    editItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialogDelete = true;
    },

    deleteItemConfirm() {
      this.desserts.splice(this.editedIndex, 1);
      this.closeDelete();
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    closeDelete() {
      this.dialogDelete = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.desserts[this.editedIndex], this.editedItem);
      } else {
        this.desserts.push(this.editedItem);
      }
      this.close();
    },
  },
};
</script>