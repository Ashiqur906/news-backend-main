<template>
  <v-row dense>
    <v-col class="col-12">

      <v-card class="mx-auto">
        <v-toolbar
          color="indigo font-weight-regular"
          dark
          dense
        >
          <v-toolbar-title>Feature Image</v-toolbar-title>
        </v-toolbar>
        <v-card>
          <v-container fluid>
            <v-row dense>
              <v-col class="col-12">

                <vue-dropzone ref="myVueDropzone" id="dropzone" :options="dropzoneOptions"></vue-dropzone>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-card>
    </v-col>
  </v-row>
</template>
<script>
import vue2Dropzone from 'vue2-dropzone'
import 'vue2-dropzone/dist/vue2Dropzone.min.css'
// import axios from 'axios'
export default {
  data: () => ({
    images: [],
    dropzoneOptions: {
      url: 'https://httpbin.org/post',
      thumbnailWidth: 150,
      maxFilesize: 0.5,
      headers: { "My-Awesome-Header": "header value" }
    }

  }),
  components: {
    vueDropzone: vue2Dropzone,
  },
  
  methods: {
    getFiles(){

    }
  },
}
</script>
