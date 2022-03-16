<template>
  <v-row ref="form">
    <v-col class="col">
      <v-container fluid>
        <v-row dense>
          <v-col class="col-12">
            <v-card
              class="mx-auto"
            >
              <!-- Current Widget : {{ current_widget }}<br>
              Selected Taxonomy  : {{ selected_taxonomy }}<br> -->
              <!-- Tax Response: {{ widgets[0] }} -->
              <!-- data: {{ data }} -->
              <v-toolbar
                color="indigo"
                class="font-weight-regular"
                dark
                dense
              >
                <v-btn text>
                  Widget Space : 
                  {{$route.params.widget_space_id}}
                </v-btn>
              </v-toolbar>
              <!-- <v-container fluid v-if="layouts"> -->
              <v-container fluid >
                <v-row dense>
                  <v-col
                    class="col-12"
                  >
                    <v-card>
                      <v-card-text>
                        <!-- Widge Select Section Start -->
                        <v-row align="center" dense>
                          <v-col
                            class=""
                            cols=""
                            sm=""
                          >
                          <!-- {{ widgetObject }} -->
                            <v-select
                              :items="widgets"
                              :item-text="'name'"
                              :item-value="'path'"
                              v-model= "widget"
                              label="Select a Widget"
                              @change="chagneData(), widgetObject = widgets.find(obj => obj.path == widget)"
                              outlined
                            ></v-select>
                          </v-col>
                        </v-row>
                        <!-- Widge Select Section End -->
                        <!-- {{ widgetObject.limit_required}} -->
                        <!-- Taxonomy Start -->
                        <v-row >
                          <!-- Select Taxonomy start -->
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if=" widgetObject.limit_required == 1"
                          >
                            <v-select
                              :items="taxonomy"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "selected_taxonomy"
                              @change="getTaxonomy"
                              label="Select a Taxonomy"
                              outlined
                            ></v-select>
                          </v-col>
                          <!-- Select Taxonomy End -->
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="selected_taxonomy === 'tag'"
                          >
                            <v-select
                              :items="tax_res"
                              :item-text="'title'"
                              :item-value="'id'"
                              v-model= "data"
                              label="Select a Tag"
                              outlined
                            ></v-select>
                          </v-col>
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="selected_taxonomy === 'category'"
                          >
                            <v-select
                              :items="tax_res"
                              :item-text="'title'"
                              :item-value="'id'"
                              v-model= "data"
                              label="Select a Category"
                              outlined
                            ></v-select>
                          </v-col>
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="selected_taxonomy === 'post'"
                          >
                            <v-select
                              :items="post"
                              :item-text="'title'"
                              :item-value="'id'"
                              v-model= "data"
                              label="Select a Post"
                              outlined
                            ></v-select>
                          </v-col>
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="widgetObject.limit_required === 1 || widgetObject.widget_type==='multiple-post'|| 
                            widgetObject.widget_type==='marquee'"
                            
                          >
                            <v-text-field
                              v-model= "data_limit"
                              label="Enter Limit"
                              outlined
                            ></v-text-field>
                          </v-col>
                        <!-- Select Taxonomy Data End -->  
                        </v-row>
                        <!-- Taxonomy End -->
                        <v-row align="center" dense v-if="widgetObject">
                          <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="widgetObject.widget_type==='html'"
                          >
                            <v-textarea
                              v-model="data"
                              label="Data"
                              outlined
                            ></v-textarea>
                          </v-col>
                          <!-- Post Section End -->
                        </v-row>
                        <!-- {{selected_post}} -->
                        <v-row align="center" dense>
                          
                          <!-- Single Post Start -->
                          <!-- <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="widgetObject.widget_type==='single-post'"
                          >
                            <v-text-field
                              :items="single_post"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "data"
                              label="Enter Post ID"
                              outlined
                            ></v-text-field>
                          </v-col> -->
                          <!-- Single Post End -->
                          <!-- Image Start -->
                          <!-- <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="widgetObject.widget_type==='image'"
                          >
                            <v-select
                              :items="image"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "data"
                              label="Select a Picture"
                              outlined
                            ></v-select>
                          </v-col> -->
                          <!-- Image End -->
                          <!-- Category Start -->
                          <!-- <v-col
                            class=""
                            cols=""
                            sm=""
                            v-if="widgetObject.widget_type==='Category'"
                          >
                            <v-text-field
                              :items="category"
                              :item-text="'title'"
                              :item-value="'key'"
                              v-model= "data"
                              label="Category ID"
                              outlined
                            ></v-text-field>
                          </v-col> -->
                        </v-row>
                      </v-card-text>

                      <v-divider class=""></v-divider>
                      <v-card-actions>
                        <v-spacer></v-spacer>

                        <v-btn
                          color="primary"
                          text
                          @click="submit($route.params.layout_id)"
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
    data:'',
    layout_id:'',
    header_id:'',
    widget_id:'',
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
    data_type:'',
    selected_header:'',
    selected_taxonomy: null,
    taxonomy_value:null,
    // widgets: ['Header', 'Post','List','Video','Footer' ],
    widgets: [],
    widget: null,
    widgetObject: {},
    header: [
      {"title" : "Header 1", 'key' : 'header-1'},
      {"title" : "Header 2", 'key' : 'header-2'},
      {"title" : "Header 3", 'key' : 'header-3'},
    ],
    taxonomy: [
      {"title" : "Category", 'key' : 'category'},
      {"title" : "Tag", 'key' : 'tag'},
      {"title" : "Post", 'key' : 'post'},
    ],
    header_placeholder:'',
    status: ['Active','Inactive'],
    widge_status:'',
    widget_type:'',
    current_widget: null,
    autoUpdate: true,
    tax_res: [],
    post: [],

  }),

  watch: {
  },
  created() {
    // this.onChange();
    this.getWidgets();
    this.getCurrentWidget();
  },

  methods: {
    chagneData(){
      this.selected_post = null;
      this.data = null;
      this.data_limit = null;
      this.data_type = null;
      this.selected_taxonomy = null;
    },
    changeWidget(widget) {
      this.widgetObject = widgets.find(obj => obj.path == widget);
    },
    getTaxonomy(){
      console.log(this.selected_taxonomy);
      if ( this.selected_taxonomy === "category-tag" ) {
        this.$axios
        .get("/l-w-s",{ params: {taxonomy: this.selected_taxonomy} })
        .then((res) => {
          if (res.data.length === 0 || res.data.error) { 
            throw {
              statusCode: 404,
              message: "Taxonomy not found",
            };
          }
            console.log(res.data);
            this.categoty =  res.data.data;
        })
      } else if(this.selected_taxonomy === "post") {
        this.$axios
        .get("/l-w-s",{
            params: { taxonomy: this.selected_taxonomy}
          })
          .then((res) => {
            if (res.data.length === 0 || res.data.error) {
              throw {
                statusCode: 404,
                message: "Taxonomy not found",
              };
            }
            console.log(res.data);
            this.post =  res.data;
          })
      } else {
        this.$axios
        .get("/l-w-s",{
            params: { taxonomy: this.selected_taxonomy}
          })
          .then((res) => {
            if (res.data.length === 0 || res.data.error) {
              throw {
                statusCode: 404,
                message: "Taxonomy not found",
              };
            }
            console.log(res.data);
            this.tax_res =  res.data;
          })
      }
    },
    getWidgets(){
      this.$axios
      .get("/widgets", {
        })
        .then((res) => {
          if (res.data.length === 0 || res.data.error) {
            throw {
              statusCode: 404,
              message: "widgets not found",
            };
          }
          this.widgets =  res.data.data;
        })
    },
    getCurrentWidget(){
      if(this.$route.params.id!==null){
        this.$axios
          .get('/layout-widgets/'+this.$route.params.id+'/edit', {
            })
            .then((res) => {
              if (res.data.length === 0 || res.data.error) {
                throw { statusCode: 404, message: "widgets not found",};
              }
              this.current_widget = res.data.data;
              this.widget = res.data.data.widget_settings.widget_type;
              this.data = res.data.data.widget_settings.data;
              this.selected_taxonomy = res.data.data.widget_settings.taxonomy;
            })
          }    
      },
    submit () {
      try {
        if(this.$route.params.id) {
          this.$axios.post('/layout-widgets/'+ this.$route.params.id , {
            data_type: this.data_type,
            data_limit: this.data_limit,
            taxonomy: this.selected_taxonomy,
            widget_type: this.widget,
            // taxonomy: this.taxonomy_value,
            layout_id: this.$route.params.layout_id,
            widget_space_id: this.$route.params.widget_space_id,
            widget_id: this.widgetObject.id,
            id: this.$route.params.id,
            data: this.data,
            _method: 'PUT',
            widget_status: this.widget_status ==="Active" ? 1 : 0,
          })
          this.$router.push( { name: 'layout-view-id', params: { id: this.$route.params.layout_id}} );
        } else {
          this.$axios.post('/layout-widgets', {
            data_type: this.data_type,
            data_limit: this.data_limit,
            taxonomy: this.selected_taxonomy,
            widget_type: this.widget,
            layout_id: this.$route.params.layout_id,
            widget_space_id: this.$route.params.widget_space_id,
            widget_id: this.widgetObject.id,
            data: this.data,
            widget_status: this.widget_status ==="Active" ? 1 : 0,
          })
          this.$router.push( { name: 'layout-view-id', params: { id: this.$route.params.layout_id}} );
        }
      } catch (e) {
        // this.error = e.response.data.message
        console.log("Error Found");
      }
    },
  },
}
</script>