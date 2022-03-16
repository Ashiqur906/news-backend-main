<template>
  <v-row ref="form">
    <!-- Left Side -->
      <v-col class="col-8">
        <v-container fluid>
          <v-row dense>
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
              <v-toolbar-title>Post Information</v-toolbar-title>


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
                        v-model="title"
                        :rules="[() => !!title || 'Title is required']"
                        :error-messages="errorMessages"
                        label="Title"
                        @keyup="makeSlug()"
                        placeholder=""
                        required
                      ></v-text-field>
                      <v-text-field
                          label="Slug"
                          name="slug"
                          v-model="slug"
                          required
                      ></v-text-field>

                      <v-textarea
                        label="Short Description"
                        v-model="short_description"
                      ></v-textarea>
                      <h4 class="white--text"> Description</h4>
                      <br>
                      <TuiEditor
                        v-model="description"
                        preview-style="vertical"
                        height="300px"
                      />

                    </v-card-text>
                    <br>
                    <!--  Meta Info -->
                    <v-container fluid>
                      <v-row dense>
                        <v-col class="col-12">

                          <v-card class="mx-auto">
                            <v-toolbar
                              color="indigo font-weight-regular"
                              dark
                              dense
                            >
                              <v-toolbar-title>Meta Info</v-toolbar-title>
                            </v-toolbar>
                            <v-card class="overflow-auto">
                              <v-container fluid>
                                <v-row dense>
                                  <v-col class="col-5">
                                    <v-text-field
                                      label="Key"
                                      name="key"
                                      v-model="meta_key"
                                    ></v-text-field>
                                  </v-col>
                                  <v-col class="col-5">
                                    <v-text-field
                                      label="Value"
                                      name="value"
                                      v-model="meta_value"
                                    ></v-text-field>
                                  </v-col>
                                  <v-col class="col-2">
                                    <v-btn @click="add" class="primary">add</v-btn>
                                  </v-col>
                                </v-row>
                                <v-row dense v-for="(textField, i) in textFields"
                                       :key="i">
                                  <v-col class="col-5">
                                    <v-text-field
                                      label="Key"
                                      v-model="textField.meta_key"
                                    ></v-text-field>
                                  </v-col>
                                  <v-col class="col-5">
                                    <v-text-field
                                      label="Value"
                                      v-model="textField.meta_value"
                                    ></v-text-field>
                                  </v-col>
                                  <v-col class="col-2">
                                    <v-btn @click="remove(i)" class="error">delete</v-btn>
                                  </v-col>
                                </v-row>
                              </v-container>
                            </v-card>
                          </v-card>
                        </v-col>
                      </v-row>
                    </v-container>
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
      <v-col class="col-4">
        <!-- Categories -->
        <v-container fluid>
          <v-row dense>
            <v-col class="col-12">
              <v-card class="mx-auto">
          <v-toolbar
              color="indigo font-weight-regular"
              dark
              dense
            >
              <v-toolbar-title>Categories</v-toolbar-title>
            </v-toolbar>
            <v-card class="overflow-auto" max-height="150">
              <v-container fluid>
              <v-row dense>
                <v-col class="col-12" v-if="categories">
                  <v-autocomplete
                    :items="categories"
                    :filter="customFilter"
                    color="white"
                    item-text="title"
                    label="Category"
                    v-model="category_id"
                    item-value="id"
                    multiple
                    small-chips
                    dense
                    chips
                  ></v-autocomplete>
<!--                  <v-checkbox-->
<!--                    v-for="category in categories"-->
<!--                    v-model="category_id"-->
<!--                    :label="category.title"-->
<!--                    v-bind:key="category.id"-->
<!--                    :value="category.id"-->
<!--                  ></v-checkbox>-->

                </v-col>
              </v-row>
            </v-container>
            </v-card>
        </v-card>
            </v-col>
          </v-row>
        </v-container>
        <!-- Categories end -->
        <!-- Tags -->
        <v-container fluid>
          <v-row dense>
            <v-col class="col-12">
              <v-card class="mx-auto">
                <v-toolbar
                  color="indigo font-weight-regular"
                  dark
                  dense
                >
                  <v-toolbar-title>Tags</v-toolbar-title>
                </v-toolbar>
                <v-card class="overflow-auto" max-height="150">
                  <v-container fluid>
                    <v-row dense>

                      <v-col class="col-12" v-if="tags">
                        <v-autocomplete
                          :items="tags"
                          :filter="customFilter"
                          color="white"
                          item-text="title"
                          label="Tag"
                          v-model="tag_id"
                          item-value="id"
                          multiple
                          small-chips
                          dense
                          chips
                        ></v-autocomplete>
<!--                        <v-checkbox-->
<!--                          v-for="tag in tags"-->
<!--                          v-model="tag_id"-->
<!--                          :label="tag.title"-->
<!--                          v-bind:key="tag.id"-->
<!--                          :value="tag.id"-->
<!--                        ></v-checkbox>-->

                      </v-col>
                    </v-row>
                  </v-container>
                </v-card>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
        <!-- Tags end -->
        <!-- Published Type -->
        <v-container fluid>
          <v-row dense>
            <v-col class="col-12">

        <v-card class="mx-auto">
          <v-toolbar
              color="indigo font-weight-regular"
              dark
              dense
            >
              <v-toolbar-title>Published</v-toolbar-title>
            </v-toolbar>
            <v-card class="overflow-auto" max-height="150">
              <v-container fluid>
              <v-row dense>
                <v-col class="col-12">
                  <v-switch
                    v-model="status"
                    :label="status ? 'Post Active' : 'Post Inactive'"
                  ></v-switch>
                </v-col>
              </v-row>
            </v-container>
            </v-card>
        </v-card>
            </v-col>
          </v-row>
        </v-container>
        <!-- Published Type End -->
        <!-- Youtube Id -->
        <v-container fluid>

          <SocialLink/>
        </v-container>
        <!-- Youtube Id End -->
        <!-- Feature Image -->
        <v-container fluid>
          <v-row class="d-flex content-center">
            <v-col cols="col-12" class="display: contents;">
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
                         image upload start
                        <img
                          :src="imagePreview"
                          class="image-preview"
                          @click="openUpload"
                          height="150px"
                        >
                        <input
                          name="image"
                          type="file"
                          id="file-field"
                          @change="uploadPreview"
                          style="display: none">
                        <!-- image upload end -->
                      </v-col>
                    </v-row>
                  </v-container>
                </v-card>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
        <!-- Feature Image End -->
        <!-- Seo Information -->
        <v-container fluid>
          <v-row dense>
            <v-col class="col-12">
              <v-card
                class="mx-auto"
              >
                <v-toolbar
                  color="indigo font-weight-regular"
                  dark
                  dense
                >
                  <v-toolbar-title>SEO Information</v-toolbar-title>
                </v-toolbar>
                <v-container fluid>
                  <v-row dense>
                    <v-col
                      class="col-12"
                    >
                      <v-card ref="form">
                        <v-card-text>
                          <v-text-field
                            ref="meta_title"
                            v-model="meta_title"
                            :rules="[() => !!meta_title || 'Meta Title is required']"
                            :error-messages="errorMessages"
                            label="Meta Title"
                            placeholder=""
                            required
                          ></v-text-field>
                        </v-card-text>
                        <v-card-text>
                          <v-text-field
                            ref="meta_description"
                            v-model="meta_description"
                            label="Meta Description"
                          ></v-text-field>
                        </v-card-text>
                        <v-card-text>
                          <v-text-field
                            ref="meta_keywords"
                            v-model="meta_keywords"
                            label="Meta Keywords"
                          ></v-text-field>
                        </v-card-text>
                        <v-card-text>
                          <v-text-field
                            ref="canonical_url"
                            v-model="canonical_url"
                            label="Canonical URL"
                          ></v-text-field>
                        </v-card-text>
                        <v-card-text>
                          <v-text-field
                            ref="meta_type"
                            v-model="meta_type"
                            label="Meta Type"
                          ></v-text-field>
                        </v-card-text>
                        <v-card-text>
                          <v-text-field
                            ref="meta_image_link"
                            v-model="meta_image_link"
                            label="Meta Image link"
                          ></v-text-field>
                        </v-card-text>
                        <v-divider class="mt-12"></v-divider>
                      </v-card>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
        <!-- Seo Information End -->
      </v-col>

  </v-row>
</template>
<script>
export default {
  imagePreview: '/assets/images/image-plus.png',
  data: () => ({
    errorMessages: '',
    title: "",
    formHasErrors: false,
    category_id: [],
    status: true,
    slug: "",
    switch_value: null,
    imagePreview: '/assets/images/image-plus.png',
    short_description: "",
    description: "",
    thumbnail: "",
    categories: [],
    meta_key: "",
    meta_value: "",
    meta_title: "",
    meta_description: "",
    meta_keywords: "",
    canonical_url: "",
    meta_type: "",
    meta_image_link: "",
    dropzoneOptions: {
      url: 'https://httpbin.org/post',
      thumbnailWidth: 200,
      maxFilesize: 1.0,
      maxFile: 1,
      headers: { "My-Awesome-Header": "header value" }
    },
    tags: [],
    tag_id: [],
    hasSaved: false,
    model: null,
    textFields: [],
    states: [
      { name: 'Division', abbr: 'DV', id: 1 },
      { name: 'District', abbr: 'DC', id: 2 },
      { name: 'Author', abbr: 'AU', id: 3 },
    ],
    district: [
      { name: 'Dhaka', abbr: 'DH', id: 1 },
      { name: 'Chandpur', abbr: 'CP', id: 2 },
      { name: 'Cumilla', abbr: 'CU', id: 3 },
      { name: 'Rangpur', abbr: 'RP', id: 4 },
      { name: 'Barisal', abbr: 'BS', id: 5 },
      { name: 'Pabna', abbr: 'PN', id: 6 },
      { name: 'Maymansing', abbr: 'MS', id: 7 },
    ],

  }),

  watch: {
    name () {
      this.errorMessages = ''
    },
    model (val) {
      if (val.length > 5) {
        this.$nextTick(() => this.model.pop())
      }
    },
  },
  created() {
    this.getCategories();
    this.getTags();
  },

  mounted(e) {
        this.slug = this.makeSlug()
    },

  methods: {
    add () {
      this.textFields.push({
        meta_key: "",
        meta_value: "",
      })
    },
    remove (index) {
      this.textFields.splice(index, 1)
    },
    customFilter (item, queryText, itemText) {
      const textOne = item.name.toLowerCase()
      const textTwo = item.abbr.toLowerCase()
      const searchText = queryText.toLowerCase()

      return textOne.indexOf(searchText) > -1 ||
        textTwo.indexOf(searchText) > -1
    },
    save () {
      this.hasSaved = true
    },
    async getCategories() {
      this.$axios
        .get('/categories')
        .then(response => {
          this.categories = response.data.data;
        })
        .catch();
    },
    async getTags() {
      this.$axios
        .get('/tags')
        .then(response => {
          this.tags = response.data;
        })
        .catch();
    },
    openUpload(){
      document.getElementById("file-field").click();
    },
    uploadPreview(e){
      // console.log('Working');
      var reader, files = e.target.files;
      if (files.length === 0){
        console.log("empty");
      }else{
        this.thumbnail = files[0];
      }
      reader = new FileReader()
      reader.onload = (e)=>{
        this.imagePreview = e.target.result
        // this.logo = files[0]
      }
      reader.readAsDataURL(files[0])
    },

    createPost(e) {
      if (this.title.length && this.slug.length && this.meta_title.length !== 0) {
        var formData = new FormData();
        var imagefile = document.querySelector('#file-field');
        formData.append("thumbnail[]", imagefile.files[0]);
        formData.append("title", this.title);
        formData.append("slug", this.slug);
        formData.append("short_description", this.short_description);
        formData.append("description", this.description);
        this.category_id.forEach(function(element) {
          formData.append("category_id[]", element);
        });
        this.tag_id.forEach(function(element) {
          formData.append("tag_id[]", element);
        });
        this.textFields.forEach(function(element, index) {
          formData.append("meta_key["+index+"]", element.meta_key);
          formData.append("meta_value["+index+"]", element.meta_value);
        });
        formData.append("status", this.status?1:0);
        formData.append("meta_title", this.meta_title);
        formData.append("meta_description", this.meta_description);
        formData.append("canonical_url", this.canonical_url);
        formData.append("meta_type", this.meta_type);
        formData.append("meta_image_link", this.meta_image_link);
        try {
          this.$axios.post('/posts', formData, {
            headers: {
              'Content-Type': 'multipart/form-data'
            }
          })
          this.$router.push('/post/post')
        } catch (e) {
          this.error = e.result
        }
      } else {
        alert('Please fill the required Fields')
      }


      // if (this.title.length && this.slug.length !== 0) {
      //   try {
      //     this.$axios.post('/posts', {
      //       title: this.title,
      //       slug: this.slug,
      //       short_description: this.short_description,
      //       description: this.description,
      //       category_id: this.category_id,
      //       status: this.status?1:0,
      //       thumbnail: this.thumbnail,
      //       meta_title: this.meta_title,
      //       meta_description: this.meta_description,
      //       canonical_url: this.canonical_url,
      //       meta_type: this.meta_type,
      //       meta_image_link: this.meta_image_link,
      //     }).then(this.$router.push('/post/post'))
      //
      //   } catch (e) {
      //     this.error = e.response.data.message
      //   }
      // } else {
      //   alert('Please fill the required Fields')
      // }

    },

    makeSlug(){
      this.slug = this.title.trim().toLocaleLowerCase().replaceAll(' ','-');
    },


  },
}
</script>
<style>
.tui-editor .te-md-splitter{
  width: 100%;
}
.theme--dark.v-card > .v-card__text, .theme--dark.v-card > .v-card__subtitle {
  color: rgb(18 18 18);
}
.tui-editor .te-preview-style-vertical .te-preview{
  background: #fff;
}
.tui-editor-contents p{
  color: #000;
}
.tui-editor .te-md-splitter{
  border-left: 1px solid #898787;
}
.te-toolbar-section{
  border-bottom: 1px solid #898787;
}
.tui-editor-defaultUI .te-mode-switch-section{
  border-top: 1px solid #898787;
}
.te-mode-switch .wysiwyg{
  display: none;
}
</style>


