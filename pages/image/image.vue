<style>
img{
  cursor: pointer;
}
.row{
  justify-content: center;
}
table{
  font-size: 20px;
}
</style>
<template>
  <v-row>
    <v-col
      cols="12"
      md="4"
      sm="5"
      class="text-center "
    >
      <v-card outlined  style="padding:20px; border-radius: 15px;">
        <v-card-title
          class="text-center"
          style="display: block"
        >Image Upload</v-card-title>
        <img
          :src="imagePreview"
          class="image-preview"
          @click="openUpload"
          width="50%"
        >
        <input
          name="image"
          type="file"
          id="file-field"
          @change="uploadPreview"
          style="display: none">
        <v-text-field
          :counter="254"
          label="Name"
          @keyup="makeSlug()"
          v-model="name"
          :rules="[() => !!name || 'Title is required']"
          :error-messages="errorMessages"
          required
        ></v-text-field>

        <v-text-field
          :counter="254"
          label="Slug"
          name="slug"
          v-model="slug"
          required
        ></v-text-field>
        <br>
        <v-btn class="mt-3 mb-2"
               @click="save"
        >
          Upload
        </v-btn>
      </v-card>
    </v-col>
    <v-col
      md="8"
      sm="7"
      class=""
    >
      <v-card outlined style="padding:10px; border-radius: 15px;">
        <v-data-table
          :headers="headers"
          :items="desserts"
          :search="search"
          sort-by="calories"
          class="elevation-1"
          style="font-size:20px"
        >
          <template v-slot:item.image="{item}">
            <v-img
              :lazy-src="item.image"
              height="150px"
              style="margin:5px; border-radius:10px;"
              min-width="50"
              max-width="150"
              :src="item.image"
              :alt="item.name"
            ></v-img>
          </template>
          <template v-slot:top>
            <v-toolbar
              flat
              style="border-radius:15px;"
            >
              <v-toolbar-title>Images</v-toolbar-title>
              <v-divider
                class="mx-4"
                inset
                vertical
              ></v-divider>
              <v-spacer></v-spacer>
              <v-text-field
                v-model="search"
                append-icon="mdi-magnify"
                label="Search"
                single-line
                hide-details
              ></v-text-field>
              <v-spacer></v-spacer>
              <v-dialog
                v-model="dialog"
                max-width="350px"
              >
                <!-- <template v-slot:activator="{ on, attrs }">
                  <v-btn
                    color="primary"
                    dark
                    class="mb-2"
                    v-bind="attrs"
                    v-on="on"
                  >
                    Add Image
                  </v-btn>
                </template> -->


                <v-card outlined style="border-radius:15px; display:block;">
                  <v-card-title>
                    <span class="text-h5">{{ formTitle }}</span>
                  </v-card-title>

                  <v-card-text class="text-center">
                    <v-container>
                      <v-row>
                        <input
                          name="image"
                          type="file"
                          id="file-field"
                          @change="uploadPreview"
                          style="display: none">
                      </v-row>
                      <img
                        :src="editedItem.image"
                        class="image-preview"
                        @click="openUpload"
                      >

                      <v-row>
                        <v-text-field
                          :counter="254"
                          label="Name"
                          @keyup="makeSlug"
                          v-model="editedItem.name"
                          :rules="[() => !!name || 'Title is required']"
                          :error-messages="errorMessages"
                          required
                        ></v-text-field>
                      </v-row>
                      <v-row>
                        <v-text-field
                          :counter="254"
                          label="Slug"
                          name="slug"
                          v-model="editedItem.slug"
                          required
                        ></v-text-field>


                      </v-row>
                    </v-container>
                  </v-card-text>

                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn
                      color="blue darken-1"
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
                  <v-card-title class="text-h5">Are you sure you want to delete this item?</v-card-title>
                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="blue darken-1" text @click="closeDelete">Cancel</v-btn>
                    <v-btn color="blue darken-1" text @click="deleteItemConfirm">OK</v-btn>
                    <v-spacer></v-spacer>
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </v-toolbar>
          </template>
          <template v-slot:item.actions="{ item }">
            <v-icon
              small
              class="mr-2"
              @click="editItem(item)"
            >
              mdi-pencil
            </v-icon>
            <v-icon
              small
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
      </v-card>


    </v-col>
  </v-row>
</template>

<script>
export default {
  imagePreview: '/assets/images/image-plus.png',
  data: () => ({
    dialog: false,
    dialogDelete: false,
    name: "",
    slug: "",
    errorMessages: '',
    imagePreview: '/assets/images/image-plus.png',
    search: '',
    headers: [
      { text: 'Image', value: 'image', align: 'start', sortable: false,},
      { text: 'Name', value: 'name' },
      { text: 'Slug', value: 'slug', sortable: false},
      { text: 'Url', value: 'url' },
      { text: 'Uploded On', value: 'uploaded' },
      { text: 'Actions', value: 'actions', sortable: false },
    ],
    desserts: [],
    editedIndex: -1,
    editedItem: {
      image: '/assets/images/image-plus.png',
      name: "",
      url: '',
    },
    defaultItem: {
      image: '/assets/images/image-plus.png',
      name: '',
      slug:'',
    },
  }),

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
    openUpload(){
      document.getElementById("file-field").click();
    },
    uploadPreview(e){
      console.log('Working');
      var reader, files = e.target.files
      if (files.length === 0){
        console.log("empty");
      }else{
        console.log(files[0])
      }
      reader = new FileReader()
      reader.onload = (e)=>{
        this.imagePreview = e.target.result
      }
      reader.readAsDataURL(files[0])
    },
    makeSlug(){
      this.slug = this.name.trim().toLocaleLowerCase().replaceAll(' ','-');
    },

    initialize () {
      this.desserts = [
        {
          name: 'River Image',
          slug: 'river-image',
          url: '/assets/images/river.jpe',
          image: '/assets/images/river.jpeg',
          uploaded: '13-Oct-2021',
        },
        {
          name: 'Mountain Image',
          slug: 'mountain-image',
          image: '/assets/images/mountain.jpeg',
          url: '/assets/images/mountain.jpeg',
          uploaded: '13-Oct-2021',
        },
        {
          name: 'Nature Image',
          slug: 'nature-image',
          image: '/assets/images/nature.jpeg',
          url: '/assets/images/nature.jpeg',
          uploaded: '13-Oct-2021',
        },
        {
          name: 'Sunset',
          slug: 'sunset-image',
          image: '/assets/images/sunset.jpeg',
          url: '/assets/images/sunset.jpeg',
          uploaded: '13-Oct-2021',
        },
        {
          name: 'Bridge',
          slug: 'bridge-image',
          image: '/assets/images/bridge.jpeg',
          url: '/assets/images/bridge.jpeg',
          uploaded: '13-Oct-2021',
        },
        {
          name: 'Waterfall',
          slug: 'waterfall-image',
          image: '/assets/images/waterfall.jpeg',
          url: '/assets/images/waterfall.jpeg',
          uploaded: '13-Oct-2021',
        },
      ]
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

    save (e) {
      console.log('working');
      var reader, files = e.target.files
      if (files.length === 0){
        console.log("empty");
      }else{
        console.log(files[0])
      }
      reader = new FileReader()
      reader.onload = (e)=>{
        this.imagePreview = e.target.result
      }
      reader.readAsDataURL(files[0])
      image
      //save desert
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

