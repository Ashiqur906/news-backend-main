<template>
  <v-row>
    <v-col class="col-12">
      <v-container fluid>
        <v-row dense>
          <v-col class="col-12">

       
            <v-card>
              <v-toolbar
                color="indigo"
                dark
                dense
                class="font-weight-bold"
              >
                <v-toolbar-title >Layouts Pannel</v-toolbar-title>
              </v-toolbar>
              <v-data-table
                :headers="headers"
                :items="layouts_data"
                :search="search"
                id="printMe"
              >
                
                <template v-slot:top>
                  <v-toolbar
                    flat
                  >
                    <v-text-field
                      v-model="search"
                      append-icon="mdi-magnify"
                      label="Search"
                      single-line
                      hide-details
                    ></v-text-field>

                    <v-btn icon :x-small="sizeXsm" :small="sizeSm" @click="print" class="mr-1 mr-lg-3">
                      <v-icon>{{mdiPrinter}}</v-icon>
                    </v-btn>
                  </v-toolbar>
                </template>
                <template v-slot:item.widget_status="{ item }" >
                  <v-btn
                    x-small
                    color="primary"
                    dark
                    class="mb-2"
                    v-if="item.widget_status == 1"
                  >
                    Active
                  </v-btn>
                  <v-btn
                    x-small
                    color="#F44336"
                    dark
                    class="mb-2"
                    v-else
                  >
                    Inactive
                  </v-btn>
                </template>
                <template v-slot:item.posts="{ item }">
                  <nuxt-link :to="{ name: 'layout-update-id', params: { id: item.id }}">
                      <v-icon
                        small
                        class="mr-2"
                      >
                        mdi-pencil
                      </v-icon>
                  </nuxt-link>
                </template>
                
              </v-data-table>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-col>
  </v-row>
</template>
<script>
import {mdiPrinter,} from "@mdi/js";
import Vue from 'vue';
import VueHtmlToPaper from 'vue-html-to-paper';
const options = {
  name: '_blank',
  specs: [
    'fullscreen=yes',
    'titlebar=yes',
    'scrollbars=yes'
  ],
  styles: [
    'https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css',
    'https://unpkg.com/kidlat-css/css/kidlat.css'
  ]
}
Vue.use(VueHtmlToPaper, options);
  export default {

    data: () => ({
        search: '',
        headers: [
          {
            text: 'Title',
            align: 'start',
            sortable: false,
            value: 'widget_name',
            width: "",
            overflow: "hidden",
          },
          {
            align: 'left' ,
            text: 'Widget Name',
            value: 'data_type',
            width: "",
            overflow: "hidden",
          },
          {
            align: 'left' ,
            text: 'Widget Type',
            value: 'widget_type',
            width: "",
            overflow: "hidden",
          },
          {
            align: 'left' ,
            text: 'Widget slug',
            value: 'widget_slug',
            width: "",
            overflow: "hidden",
          },
          {
            align: 'center' ,
            text: 'Status',
            value: 'widget_status',
            width: "",
            overflow: "hidden",
          },
          
          {
            align: 'center',
            text: 'Actions',
            value: 'posts',
            sortable: false,
            width: "",
            overflow: "hidden",
          },
        ],
      layouts_data: [],
     
      mdiPrinter: mdiPrinter,
      dialogDelete: false,
    }),

    created () {
      this.getLayouts();
      this.getWidget();
    },

    methods: {

      async getLayouts() {

        try {
          const {data} = await this.$axios.get('/layouts/create');
          this.posts = data;
          this.layouts_data = data;
          
        } catch (e) {
          this.error = e.data;
        }
      },
     

      print () {
        // Pass the element id here
        this.$htmlToPaper('printMe');
      },
    },
    computed: {
      sizeSm: function () {
        return this.$vuetify.breakpoint.name == 'xs' ? false : true;
      },
      sizeXsm: function () {
        return this.$vuetify.breakpoint.name == 'xs' ? true : false;
      },
    },
    
  }
</script>
<style>
.v-application a{
  text-decoration: none;
}
</style>
