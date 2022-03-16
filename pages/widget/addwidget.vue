<template>
  <v-row ref="form">
    <!-- Left Side -->
      <v-col class="col-12" >
        <v-container fluid>
          <v-row dense >
            <v-col class="col-12">
          <v-card
            class="mx-auto"
          >
            <v-toolbar
              color="indigo"
              class="font-weight-regular"
              dark
              dense
            >
              <v-toolbar-title>Widget Information</v-toolbar-title>
            </v-toolbar>
            <v-container fluid>
              <v-row dense>
                <v-col
                  class="col-12"
                >
                  <v-card>
                    <v-card-text>
                      <v-text-field
                        ref="title"
                        v-model="name"
                        :rules="[() => !!name || 'Title is required']"
                        :error-messages="errorMessages"
                        label="Title"
                        @keyup="makeSlug()"
                        placeholder=""
                        required
                      ></v-text-field>
                      <v-text-field
                          label="Path"
                          v-model="path"
                          required
                      ></v-text-field>
                      <v-select
                        :items="widgets"
                        v-model= "widget_type"
                        label="Select a Widge"
                      ></v-select>

                      <v-text-field
                        label="Data Limit"
                        v-model="data_limit"
                        required
                      ></v-text-field>
                      <v-switch
                        v-model="status"
                        :label="status ? 'Active' : ' Deactive'"
                      ></v-switch>
                      

                    </v-card-text>
                    <v-divider class="mt-12"></v-divider>
                    <v-card-actions>
                      <v-btn text>
                        Cancel
                      </v-btn>
                      <v-spacer></v-spacer>

                      <v-btn
                        color="primary"
                        text
                        @click="createPost"
                      >
                        Submit
                      </v-btn>
                    </v-card-actions>
                  </v-card>
                </v-col>
              </v-row>
            </v-container>
          </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-col>
      <!-- Right Side -->

  </v-row>
</template>
<script>
export default {
  imagePreview: '/assets/images/image-plus.png',
  data: () => ({
    errorMessages:'',
    name:'',
    path:'',
    widget_type:'',
    data_limit:'',
    status: true,
    widgets: ['Header', 'Post','Footer' ]
  }),

  watch: {
    name () {
      this.errorMessages = ''
    },
  },

  mounted(e) {
    this.slug = this.makeSlug()
  },

  methods: {
    async getCategories() {
      this.$axios
        .get('/categories')
        .then(response => {
          this.categories = response.data;
        })
        .catch();
    },

    createPost(e) {
      console.log('data limit:', this.data_limit);
      if (this.name.length && this.path.length !== 0) {
        var formData = new FormData();
        // var imagefile = document.querySelector('#file-field');
        formData.append("name", this.name);
        formData.append("path", this.path);
        formData.append("widget_type", this.widget_type);
        formData.append("data_limit", this.data_limit);
        formData.append("status", this.status==true?1:0);
        try {
          this.$axios.post('/widgets', formData, {}),
          this.$router.push('/widget/list')
        } catch (e) {
          this.error = e.result
        }
      } else {
        alert('Please fill the required Fields')
      }
    },
    makeSlug(){
      this.path = this.name.trim().toLocaleLowerCase().replaceAll(' ','-');
    },
  },
}
</script>


