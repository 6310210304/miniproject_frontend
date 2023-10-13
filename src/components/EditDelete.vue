<template>
<div>
  <v-data-table
    :headers="headers"
    :items="desserts"
    class="elevation-1"
  >
    <template v-slot:top>
      <v-toolbar
        flat
      >
        <v-toolbar-title>จัดการข้อมูล</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>
        <v-dialog
          v-model="dialog"
          max-width="500px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="primary"
              dark
              class="mb-2"
              v-bind="attrs"
              v-on="on"
            >
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
                  <v-col
                    cols="1"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.name"
                      label="Name"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.picture"
                      label="Picture"
                    ></v-text-field>
                  </v-col>
                  <v-col
                    cols="12"
                    sm="6"
                    md="4"
                  >
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
              <v-btn
                color="red darken-1"
                text
                @click="close"
              >
                Cancel
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="save"
              >
                Save
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="text-h5">คุณแน่ใจหรือว่าต้องการลบรายการนี้?</v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="closeDelete">Cancel</v-btn>
              <v-btn color="red darken-1" text @click="deleteItemConfirm">OK</v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>


    </template>
    <template v-slot:item.picture="{ item }">
      <v-img
        :src="item.picture"
        :alt="item.name"
        max-width="200"
      ></v-img>

      <v-icon
        color="yellow darken-1"
        big
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        color="red darken-1"
        big
        @click="deleteItem(item)"
      >
        mdi-delete
      </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn
        color="primary"
        @click="initialize"
      >
        Reset
      </v-btn>
    </template>
  </v-data-table>
</div>
</template>


<script>
  export default {
    data: () => ({
      dialog: false,
      dialogDelete: false,
      headers: [
        {
            text: 'Name',
            align: 'start',
            sortable: false,
            value: 'name',
        },
        {
            text: 'Picture',
            value: 'picture',
            // เพิ่ม scopedSlots เพื่อแสดงรูปภาพ
            scopedSlots: { custom: 'picture' },
        },
        {
            text: 'Description',
            value: 'description',
        },
      ],

      desserts: [],
      editedIndex: -1,
      editedItem: {
        name: '',
        calories: 0,
        fat: 0,
        carbs: 0,
        protein: 0,
      },
      defaultItem: {
        name: '',
        calories: 0,
        fat: 0,
        carbs: 0,
        protein: 0,
      },
    }),
    scopedSlots: {
      picture: (item) => {
        return this.$createElement('img', {
          attrs: {
            src: item.picture, // ใช้ URL รูปภาพจากข้อมูล
            alt: item.name, // ใช้ชื่อเป็นคำอธิบายรูปภาพ
            style: 'max-width: 100px;', // กำหนดขนาดสูงสุดของรูปภาพ
          },
        });
      },
    },

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
      },
    },

    watch: {
      dialog (val) {
        val || this.close()
      },
      dialogDelete (val) {
        val || this.closeDelete()
      },
    },

    created () {
      this.initialize()
    },

    methods: {

      initialize() {
        this.desserts = [
          {
            name: 'ตึกฟิสิกส์',
            // รูปภาพในรูปแบบ URL
            picture: 'https://www.hatyaifocus.com/ckeditor/upload/forums/1/%E0%B9%82%E0%B8%9A%E0%B9%89/%E0%B8%AA%E0%B8%84./%E0%B9%82%E0%B8%A3%E0%B8%87%E0%B8%AD%E0%B8%B2%E0%B8%AB%E0%B8%B2%E0%B8%A3%E0%B8%9F%E0%B8%B4%E0%B8%AA%E0%B8%B4%E0%B8%81/118175476_3263028410441578_2379294325614708343_o.jpg',
            description: 'เรียกได้ว่าเป็น "โรงอาหารคณะวิทยาศาสตร์" ร้านอาหารต่างๆขายช่วงเช้าถึงบ่ายโมง',
          },
          {
            name: 'ตึกBSc',
            picture: 'https://www.sci.psu.ac.th/wp-content/uploads/2022/06/5-places-to-chill-out-3.jpg',
            description: 'มีเซเว่น ร้านขายข้าวไข่เจียว และร้านไก่ย่าง5ดาว ก่อนเรียนหรือเรียนเสร็จนักศึกษามักจะมานั่งรับประทานอาหารกัน',
          },
          {
            name: 'ตึกBSc',
            picture: 'https://scontent-kul2-2.xx.fbcdn.net/v/t1.6435-9/165662959_2806995216296697_5027621551341281790_n.jpg?_nc_cat=103&ccb=1-7&_nc_sid=8bfeb9&_nc_eui2=AeFEjn0PsWTIw_urIoiE0dN5A3pFiNAh0e4DekWI0CHR7l1UG9XBou2d10MxAnMP1zuzHYf-yeDomU1VEBjqRRau&_nc_ohc=Jp2oiXCPD2IAX-39uwT&_nc_ht=scontent-kul2-2.xx&oh=00_AfD9Df0wUEQ0U0XRq7rOgVCt9l1VY-iAvCTL98TF5RtZOA&oe=653F8FAF',
            description: 'ร้าน etc. เป็นคาเฟ่เล็กๆ มีอาหาารอร่อยๆหลายเมนู สามารถนั่งรับประทานในร้านเพื่อตากแอร์เย็นๆ หรือนั่งข้างนอกเพื่อรับลมธรรมชาติก็ได้',
          },
        ];
      },

      computed: {
        formTitle() {
            return this.editedIndex === -1 ? 'New Item' : 'Edit Item';
        },
      },

      editItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialogDelete = true
      },

      deleteItemConfirm () {
        this.desserts.splice(this.editedIndex, 1)
        this.closeDelete()
      },

      close () {
        this.dialog = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      closeDelete () {
        this.dialogDelete = false
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      save () {
        if (this.editedIndex > -1) {
          Object.assign(this.desserts[this.editedIndex], this.editedItem)
        } else {
          this.desserts.push(this.editedItem)
        }
        this.close()
      },
    },
  }
</script>