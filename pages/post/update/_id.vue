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
                <v-toolbar-title>Post Edit</v-toolbar-title>


              </v-toolbar>
              <!--{{post}}-->
              <v-container
                fluid
                v-if="post"
              >
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
                          @keyup="slug = title.trim().toLocaleLowerCase().replaceAll(' ','-')"
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
                          name="short_description"
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
                      <v-container fluid v-if="post['postMeta']">
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
                                  <v-row dense v-for="(textField, i) in post['postMeta']"
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
                      <!--  Meta Info end -->
                      <v-divider class="mt-12"></v-divider>
                      <v-card-actions>
                        <v-btn text>
                          Cancel
                        </v-btn>
                        <v-spacer></v-spacer>

                        <v-btn
                          color="primary"
                          text
                          @click="submit"
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
<!--                    {{categories}}-->
                    <v-col class="col-12" v-if="category_id == null">
                      <v-autocomplete
                        :items="category_id"
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
                    </v-col>
                    <v-col class="col-12" v-else>
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
                <v-toolbar-title>Categories</v-toolbar-title>
              </v-toolbar>

              <v-card class="overflow-auto" max-height="150">
                <v-container fluid>
                  <v-row dense>
                    <v-col class="col-12" v-if="tag_id == null">
                      <v-autocomplete
                        :items="tag_id"
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

                    </v-col>
                    <v-col class="col-12" v-else>
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
                        :label="status ? 'Post Active' : 'Post Deactive'"
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
<!--      {{imagePreview[0]['id']}}}-->
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
                        :src="imagePreview[0]?imagePreview[0]['thumbnail']: imageToPreview"
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
                          ref="seo['meta_title']"
                          v-model="seo['meta_title']"
                          :rules="[() => !!seo['meta_title'] || 'Meta Title is required']"
                          :error-messages="errorMessages"
                          label="Meta Title"
                          placeholder=""
                          required
                        ></v-text-field>

                      </v-card-text>
                      <v-card-text>
                        <v-text-field
                          ref="seo['meta_description']"
                          v-model="seo['meta_description']"
                          label="Meta Description"
                        ></v-text-field>

                      </v-card-text>
                      <v-card-text>
                        <v-text-field
                          ref="seo['meta_keywords']"
                          v-model="seo['meta_keywords']"
                          label="Meta Keywords"
                        ></v-text-field>

                      </v-card-text>
                      <v-card-text>
                        <v-text-field
                          ref="seo['canonical_url']"
                          v-model="seo['canonical_url']"
                          label="Canonical URL"
                        ></v-text-field>

                      </v-card-text>
                      <v-card-text>
                        <v-text-field
                          ref="seo['meta_type']"
                          v-model="seo['meta_type']"
                          label="Meta Type"
                        ></v-text-field>

                      </v-card-text>
                      <v-card-text>
                        <v-text-field
                          ref="seo['meta_image_link']"
                          v-model="seo['meta_image_link']"
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
  data: () => ({
    errorMessages: '',
    title: "",
    formHasErrors: false,
    category_id: [],
    status: true,
    categories: [],
    statusCode: null,
    slug: "",
    id: "",
    short_description: "",
    description: "",
    thumbnail: "",
    meta_key: "",
    meta_value: "",
    seo: "",
    meta_title: "",
    meta_description: "",
    meta_keywords: "",
    canonical_url: "",
    meta_type: "",
    meta_image_link: "",
    imageToPreview: '/assets/images/image-plus.png',
    imagePreview: '/assets/images/image-plus.png',
    dropzoneOptions: {
      url: 'https://httpbin.org/post',
      thumbnailWidth: 200,
      maxFilesize: 1.0,
      maxFile: 1,
      headers: { "My-Awesome-Header": "header value" }
    },
    hasSaved: false,
    model: null,
    tags: [],
    tag_id: [],
    post_metas: [],
    textFields: [],
  }),

  watch: {
    name () {
      this.errorMessages = ''
    },
  },
  created() {
    this.getCategories();
    this.getTags();
  },

  methods: {
    add () {
      this.post['postMeta'].push({
        meta_key: "",
        meta_value: "",
      })
    },
    remove (index) {
      this.post['postMeta'].splice(index, 1)
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

    submit () {
      // console.log(this.thumbnail);
      if (this.title.length && this.slug.length !== 0) {
        var formData = new FormData();
        var imagefile = document.querySelector('#file-field');
        formData.append("thumbnail[]", imagefile.files[0]);
        formData.append("_method", 'PUT');
        formData.append("id", this.$route.params.id);
        formData.append("title", this.title);
        formData.append("slug", this.slug);
        formData.append("short_description", this.short_description);
        formData.append("description", this.description);
        this.category_id.forEach(function(element) {
          formData.append("category_id[]", element);
        });
        this.post['postMeta'].forEach(function(element, index) {
          formData.append("meta_key["+index+"]", element.meta_key);
          formData.append("meta_value["+index+"]", element.meta_value);
        });
        this.tag_id.forEach(function(element) {
          formData.append("tag_id[]", element);
        });
        formData.append("status", this.status?1:0);
        formData.append("meta_title", this.seo['meta_title']);
        formData.append("meta_description", this.seo['meta_description']);
        formData.append("canonical_url", this.seo['canonical_url']);
        formData.append("meta_type", this.seo['meta_type']);
        formData.append("meta_image_link", this.seo['meta_image_link']);
        try {
          this.$axios.post('/posts/'+this.$route.params.id, formData, {
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
      /*if (this.title.length && this.slug.length !== 0) {
      // if (this.title.lif (this.title.length && this.slug.length !== 0) {
        var formData = new FormData();
        var imagefile = document.querySelector('#file-field');
        formData.append("id", this.$route.params.id);
        formData.append("title", this.title);
        formData.append("slug", this.slug);
        formData.append("short_description", this.short_description);
        formData.append("description", this.description);
        formData.append("thumbnail[]", imagefile.files[0]);
        formData.append("category_id[]", this.category_id);
        formData.append("tag_id[]", this.tag_id);
        formData.append("status", this.status?1:0);
        formData.append("meta_title", this.meta_title);
        formData.append("meta_description", this.meta_description);
        formData.append("canonical_url", this.canonical_url);
        formData.append("meta_type", this.meta_type);
        formData.append("meta_image_link", this.meta_image_link);
        try {
          this.$axios.put('/posts/'+this.$route.params.id, formData, {
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
      }*/
/*
      try {
        this.$axios.put('/posts/'+ this.$route.params.id, {
          thumbnail: this.thumbnail,
          id: this.$route.params.id,
          title: this.title,
          slug: this.slug,
          short_description: this.short_description,
          description: this.description,
          category_id: this.category_id,
          tag_id: this.tag_id,
          status: this.status?1:0,
          meta_title: this.seo['meta_title'],
          meta_description: this.seo['meta_description'],
          canonical_url: this.seo['canonical_url'],
          meta_type: this.seo['meta_type'],
          meta_image_link: this.seo['meta_image_link'],
        })

        this.$router.push('/post/post')
      } catch (e) {
        this.error = e.response.data.message
      }*/
    },

  },
  asyncData(context) {
    const AuthStr = 'Bearer '.concat(context.$auth.strategy.token.get());
    return context.$axios
      .get('/posts/' + context.params.id + '/edit', { headers: { Authorization: AuthStr } })
      .then((res) => {
        if (res.data.length === 0 || res.data.error) {
          throw({ statusCode: 404, message: 'Post not found' })
        }
        return { post: res.data.post, title: res.data.post.title, id: res.data.post.id, slug: res.data.post.slug,
          short_description: res.data.post.short_description, description: res.data.post.description,
          imagePreview: res.data.post.pictures, status: res.data.post.status, seo: res.data.post.seo,
          category_id: res.data.post.categories, tag_id: res.data.post.tags, postMeta: res.data.post.postMeta
        }
      })
      .catch(error => {
        if (error.response) {
          // Request made and server responded
          this.errorCode = error.response.status;
        } else if (error.request) {
          // The request was made but no response was received
        } if (error.statusCode === 404) {
          return context.error({ statusCode: 404, message: error.message })
        } else {
          // Something happened in setting up the request that triggered an Error
          return {error: error.message};
          return context.error({ statusCode: 500, message: error.message })
        }
      });
  },
}
</script>
<style>
.tui-editor .te-md-splitter{
  width: 100%;
}
.theme--dark.v-card > .v-card_text, .theme--dark.v-card > .v-card_subtitle {
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
.CodeMirror-vscrollbar, .CodeMirror-hscrollbar, .CodeMirror-scrollbar-filler, .CodeMirror-gutter-filler{
  z-index: 1;
}
</style>