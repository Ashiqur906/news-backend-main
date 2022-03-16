<template>
  <v-row ref="form">
    <v-col class="col">
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
                <v-btn text>
                  Widget Space : 
                  {{layouts.id}}
                </v-btn>
              </v-toolbar>

              <v-container fluid v-if="layouts">
                <v-row dense>
                  <v-col
                    class="col-12"
                  >
                    <v-card>
                      <v-card-text>
                        <!-- Widge Type Section Start -->
                        <v-row align="center" dense>
                          <v-col
                            class=""
                            cols=""
                            sm=""
                          >
                            <v-select
                              :items="widgets"
                              v-model= "data_type"
                              label="Select a Widge"
                              @change="onChange"
                              outlined
                            ></v-select>
                          </v-col>
                        </v-row>
                        <!-- Widge Type Section End -->
                        <v-row align="center" dense>
                          <!-- Header Section Start -->
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="data_type==='Header'"
                          >
                            <v-select
                              :items="header"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "widget_type"
                              label="Select a Header"
                              outlined
                            ></v-select>
                          </v-col>
                          <!-- Header Section End -->
                          <!-- Footer Section Start -->
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="data_type==='Footer'"
                          >
                            <v-select
                              :items="footer"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "widget_type"
                              label="Select a Footer"
                              outlined
                            ></v-select>
                          </v-col>
                          <!-- Footer Section End -->
                          <!-- Post Section Start -->
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="data_type==='Post'"
                          >
                            <v-select
                              :items="post"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "selected_post"
                              label="Select a Post"
                              outlined
                            ></v-select>
                          </v-col>
                          <!-- Post Section End -->
                        </v-row>
                        <!-- {{selected_post}} -->
                        <v-row align="center" dense>
                          <!-- Single Post Start -->
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="selected_post==='single-post'"
                          >
                            <v-text-field
                              :items="single_post"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "single_post_id"
                              label="Enter Post ID"
                              outlined
                            ></v-text-field>
                          </v-col>
                          <!-- Single Post End -->
                          <!-- Multiple Post Start -->
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="selected_post==='multiple-post'"
                          >
                            <v-select
                              :items="multiple_post"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "multiple_post_data_limit"
                              label="Enter Limit"
                              outlined
                            ></v-select>
                          </v-col>
                          <!-- Multiple Post End -->
                          <!-- Image Start -->
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="selected_post==='image'"
                          >
                            <v-select
                              :items="image"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "selected_image"
                              label="Select a Picture"
                              outlined
                            ></v-select>
                          </v-col>
                          <!-- Image End -->
                          <!-- Category Start -->
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="selected_post==='category'"
                          >
                            <v-text-field
                              :items="category"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "category_id"
                              label="Category ID"
                              outlined
                            ></v-text-field>
                          </v-col>
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="selected_post==='category'"
                          >
                            <v-text-field
                              :items="category"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "category_limit"
                              label="Category Limit"
                              outlined
                            ></v-text-field>
                          </v-col>
                          <!-- Category End -->
                          <!-- Tag Start -->
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="selected_post==='tag'"
                          >
                            <v-text-field
                              :items="tag"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "tag_id"
                              label="Tag ID"
                              outlined
                            ></v-text-field>
                          </v-col>
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="selected_post === 'tag'"
                          >
                            <v-text-field
                              :items="tag"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "tag_limit"
                              label="Tag Limit"
                              outlined
                            ></v-text-field>
                          </v-col>
                          <!-- Tag End -->
                        </v-row>
                      </v-card-text>

                      <v-divider class=""></v-divider>
                      <v-card-actions>
                        <v-spacer></v-spacer>

                        <v-btn
                          color="primary"
                          text
                          @click="submit(layouts.layout_slug)"
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
  </v-row>
</template>
<script>
export default {
  data: () => ({
    header_id:'',
    selected_post:'',
    selected_image:'',
    tag_id:'',
    tag_limit:'',
    category_id:'',
    category_limit:'',
    single_post_id:'',
    multiple_post_data_limit:'',
    selected_status:'',
    selected_body:'',
    data_limit:'',
    selected_header:'',
    widgets: ['Header', 'Post','List','Video','Footer' ],
    header: [
      {"title" : "Header 1", 'key' : 'header-1'},
      {"title" : "Header 2", 'key' : 'header-2'},
      {"title" : "Header 3", 'key' : 'header-3'},
    ],
    post: [
      {"title" : "Single Post", 'key' : 'single-post'},
      {"title" : "Multiple Post", 'key' : 'multiple-post'},
      {"title" : "Image", 'key' : 'image'},
      {"title" : "Category", 'key' : 'category'},
      {"title" : "Tag", 'key' : 'tag'},
    ],
    single_post: [
      {"title" : "Single Post 1", 'key' : 'single-post-1'},
      {"title" : "Single Post 2", 'key' : 'single-post-2'},
      {"title" : "Single Post 3", 'key' : 'single-post-3'},
      {"title" : "Single Post 4", 'key' : 'single-post-4'},
      {"title" : "Single Post 5", 'key' : 'single-post-5'},
    ],
    multiple_post: [
      {"title" : "Multiple Post 1", 'key' : 'multiple-post-1'},
      {"title" : "Multiple Post 2", 'key' : 'multiple-post-2'},
      {"title" : "Multiple Post 3", 'key' : 'multiple-post-3'},
      {"title" : "Multiple Post 4", 'key' : 'multiple-post-4'},
      {"title" : "Multiple Post 5", 'key' : 'multiple-post-5'},
    ],
    image: [
      {"title" : "Picture 1", 'key' : 'picture-1'},
      {"title" : "Picture 2", 'key' : 'picture-2'},
      {"title" : "Picture 3", 'key' : 'picture-3'},
      {"title" : "Picture 4", 'key' : 'picture-4'},
      {"title" : "Picture 5", 'key' : 'picture-5'},
    ],
    category: [
      {"title" : "Category 1", 'key' : 'catrgory-1'},
      {"title" : "Category 2", 'key' : 'catrgory-2'},
      {"title" : "Category 3", 'key' : 'catrgory-3'},
      {"title" : "Category 4", 'key' : 'catrgory-4'},
      {"title" : "Category 5", 'key' : 'catrgory-5'},
    ],
    tag: [
      {"title" : "Tag 1", 'key' : 'tag-1'},
      {"title" : "Tag 2", 'key' : 'tag-2'},
      {"title" : "Tag 3", 'key' : 'tag-3'},
      {"title" : "Tag 4", 'key' : 'tag-4'},
      {"title" : "Tag 5", 'key' : 'tag-5'},
    ],
    footer: [
      {"title" : "Footer 1", 'key' : 'footer-1'},
      {"title" : "Footer 2", 'key' : 'footer-2'},
      {"title" : "Footer 3", 'key' : 'footer-3'},
    ],
    // widget_type : 'header-2',
    //body: [
    //{ name: 'Header One', avatar: 'http://localhost:3000/assets/images/mountain.jpeg' },
    //{ name: 'Header Two', avatar: 'https://cdn.vuetifyjs.com/images/lists/1.jpg' },
    //{ name: 'Sigle Post (without short description)', avatar: 'http://localhost:3000/assets/images/river.jpeg' },
    //{ name: 'Single Post (with short description)', avatar: 'http://localhost:3000/assets/images/images.jpeg' },
    //{ name: 'Single Post (right side image)', avatar: 'http://localhost:3000/assets/images/river.jpeg' },
    //{ name: 'Single Post (left side image)', avatar: 'https://cdn.vuetifyjs.com/images/lists/4.jpg' },
    //{ name: 'Single Post (left side title)', avatar: 'https://cdn.vuetifyjs.com/images/lists/3.jpg' },
    //{ name: 'Single Post (right side title)', avatar: 'https://cdn.vuetifyjs.com/images/lists/5.jpg' },
    //{ name: 'Multiple Post (with highlight)', avatar: 'https://cdn.vuetifyjs.com/images/lists/5.jpg' },
    //{ name: 'Multiple Post', avatar: 'https://cdn.vuetifyjs.com/images/lists/5.jpg' },
    //{ name: 'Slider', avatar: 'https://cdn.vuetifyjs.com/images/lists/5.jpg' },
    //{ name: 'Advertisement', avatar: 'https://cdn.vuetifyjs.com/images/lists/5.jpg' },
    //],
    header_placeholder:'',
    status: ['Active','Inactive'],
    widge_status:'',
    autoUpdate: true,

  }),

  watch: {
    name () {
      this.errorMessages = ''
    },
  },
  created() {
    this.onChange();
  },

  methods: {

    submit (slug) {
      // console.log(this.widget_type);
      try {

        this.$axios.put('/widgets/'+ this.$route.params.id, {
          data_type: this.data_type,
          data_limit: this.data_limit,
          widget_type: this.widget_type,
          widget_status: this.widget_status ==="Active" ? 1 : 0,
        })
        this.$router.push( { name: 'layout-view-slug', params: { slug: slug }} );
      } catch (e) {
        this.error = e.response.data.message
      }
    },

    onChange(){
      this.selected_post = '';
    }
  },
  asyncData(context) {
    const AuthStr = 'Bearer '.concat(context.$auth.strategy.token.get());
    return context.$axios
      .get('/widgets/' + context.params.id + '/edit', { headers: { Authorization: AuthStr } })
      .then((res) => {
        if (res.data.length === 0 || res.data.error) {
          throw({ statusCode: 404, message: 'Post not found' })
        }
        return { layouts: res.data, data_type: res.data.data_type, data_limit: res.data.data_limit, widget_type: res.data.widget_type, widget_status: res.data.widget_status === 1 ? 'Active':'Inactive' }
      })
      .catch(error => {
        if (error.response) {
          // Request made and server responded
          this.errorCode = error.response.status;
        } else if (error.request) {
          // The request was made but no response was received
        }

        if (error.statusCode === 404) {
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
