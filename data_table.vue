<template>
  <v-data-table
    :headers="computedHeaders"
    :items="filteredDesserts"
    :sort-by="[{ key: 'calories', order: 'asc' }]"
  >
    <template v-slot:top>
      <v-toolbar flat>
        <v-toolbar-title>รายชื่อสมาชิก</v-toolbar-title>
        <v-divider class="mx-4" inset vertical></v-divider>
        <v-spacer></v-spacer>

        <div class="search">
          <!-- ช่องค้นหา -->
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="ค้นหา"
            class="search-field"
          ></v-text-field>
        </div>

        <v-dialog v-model="dialog" max-width="500px">
          <template v-slot:activator="{ props }">
            <v-btn class="mb-2 primary" dark v-bind="props">
              เพิ่มข้อมูล
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="text-h5">{{ formTitle }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <!-- ฟิลด์ที่ใช้เพิ่มหรือแก้ไขข้อมูล -->
                  <v-col cols="12" md="4" sm="6">
                    <v-text-field
                      v-model="editedItem.id"
                      label="id"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" md="4" sm="6">
                    <v-text-field
                      v-model="editedItem.username"
                      label="username"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" md="4" sm="6">
                    <v-text-field
                      v-model="editedItem.password"
                      label="password"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" md="4" sm="6">
                    <v-text-field
                      v-model="editedItem.email"
                      label="email"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" md="4" sm="6">
                    <v-text-field
                      v-model="editedItem.status"
                      label="status"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" md="4" sm="6">
                    <v-file-input
                      label="Upload Picture"
                      accept="image/*"
                      prepend-icon="mdi-camera"
                      @change="handleFileUpload"
                    ></v-file-input>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn class="cancel-btn" variant="text" @click="close">
                Cancel
              </v-btn>
              <v-btn class="save-btn" variant="text" @click="save">
                Save
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>

        <v-dialog v-model="dialogDelete" max-width="500px">
          <v-card>
            <v-card-title class="text-h5">
              คุณแน่ใจหรือไม่ที่จะลบข้อมูลนี้?
            </v-card-title>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn class="cancel-btn" variant="text" @click="closeDelete">
                Cancel
              </v-btn>
              <v-btn class="save-btn" variant="text" @click="deleteItemConfirm">
                OK
              </v-btn>
              <v-spacer></v-spacer>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>
    </template>

    <template v-slot:item.actions="{ item }" >
      <v-icon class="me-2 my-custom-edit-icon" size="small" @click="editItem(item)">
        mdi-pencil
      </v-icon>
      <v-icon class="my-custom-delete-icon" size="small" @click="deleteItem(item)"> mdi-delete </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn class="primary" @click="initialize"> Reset </v-btn>
    </template>
  </v-data-table>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    dialog: false,
    dialogDelete: false,
    search: '',
    headers: [
      { title: 'id', align: 'start', sortable: false, key: 'id' },
      { title: 'username', key: 'username' },
      { title: 'password', key: 'password' },
      { title: 'email', key: 'email' },
      { title: 'status', key: 'status' },
      { title: 'picture', key: 'picture' },
      { title: 'Edit/Del', key: 'actions', sortable: false },
    ],
    desserts: [],
    editedIndex: -1,
    editedItem: {
      id: '',
      username: '',
      password: '',
      email: '',
      status: '',
      picture: '', // This will store the file name or base64 encoded image
    },
    defaultItem: {
      id: '',
      username: '',
      password: '',
      email: '',
      status: '',
      picture: '',
    },
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? 'เพิ่มข้อมูล' : 'แก้ไขข้อมูล';
    },
    computedHeaders() {
      return this.headers;
    },
    filteredDesserts() {
      if (this.search) {
        return this.desserts.filter(dessert => {
          return Object.values(dessert).some(value =>
            String(value).toLowerCase().includes(this.search.toLowerCase())
          );
        });
      }
      return this.desserts;
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

  async created() {
    this.fetchData();
  },

  methods: {
    initialize() {
      this.desserts = [];
    },

    editItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
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

    async save() {
  if (this.editedIndex > -1) {
    try {
      const response = await axios.post("http://localhost:7000/update", this.editedItem);
      const data = response.data;
      console.log(data);
      if (data.ok) {
        Object.assign(this.desserts[this.editedIndex], this.editedItem);
        alert('Item updated successfully');
      } else {
        alert(data.error); // Show the error message returned from the server
      }
    } catch (error) {
      console.error('Error updating item:', error);
      alert(error.message || 'An error occurred while updating the item');
    }
  } else {
    try {
      const response = await axios.post("http://localhost:7000/insert", this.editedItem);
      const data = response.data;
      console.log(data);
      if (data.ok) {
        this.desserts.push(this.editedItem);
        alert('Item added successfully');
      } else {
        alert(data.error); // Show the error message returned from the server
      }
    } catch (error) {
      console.error('Error adding item:', error);
      alert(error.message || 'An error occurred while adding the item');
    }
  }
  this.close();
},

    async deleteItem(item) {
      if (confirm('Are you sure you want to delete this item?')) {
        try {
          const response = await axios.post("http://localhost:7000/delete", item);
          const data = response.data;
          console.log(data);
          if (data.ok) {
            this.desserts = this.desserts.filter(dessert => dessert.id !== item.id);
            alert('Item deleted successfully');
          } else {
            alert(data.error || 'Failed to delete item');
          }
        } catch (error) {
          console.error('Error deleting item:', error);
          alert(error.message || 'An error occurred while deleting the item');
        }
      }
    },

    async fetchData() {
      try {
        const response = await axios.get("http://localhost:7000/list");
        this.desserts = response.data.row;
      } catch (error) {
        console.error('Error fetching data:', error);
        alert('Failed to refresh data');
      }
    },

    handleFileUpload(event) {
  const file = event.target.files[0];
  if (file) {
    const reader = new FileReader();
    reader.onload = (e) => {
      this.editedItem.picture = e.target.result; // เก็บภาพในรูปแบบ Base64
    };
    reader.readAsDataURL(file);
  }
}
,
  },
};
</script>

<style scoped>
.v-img {
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 4px;
}

.search-field{
  padding-left: 20px;
  margin-right: 60px;
}

.search-field {
  padding-bottom: 56px;
  height: 20px;
  width: 300px;
  transition: 0.2s;
}

.v-btn {
  background-color: #2965c0;
  color: white;
}

.my-custom-edit-icon {
  color: #2965c0; /* สีเขียวสำหรับปุ่มแก้ไข */
}

.my-custom-delete-icon {
  color: #f44336; /* สีแดงสำหรับปุ่มลบ */
}

.cancel-btn {
  background-color: #f44336; /* สีแดงสำหรับปุ่มยกเลิก */
  color: white;
}

.save-btn {
  background-color: #2965c0; /* สีเขียวสำหรับปุ่มบันทึก */
  color: white;
}

.primary {
  background-color: #2965c0;
  color: white;
}

.my-custom-image {
  border: 1px solid #ddd;
  border-radius: 4px;
  padding: 4px;
}
</style>
