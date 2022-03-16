<template>
  <v-row>
    <v-col class="col-12">
      <v-container fluid v-if="seos">
        <v-row dense>
          <v-col class="col-12">
            <v-card>
              <v-toolbar
                color="indigo"
                class="font-weight-bold"
                dark
                dense
              >
                <v-toolbar-title>SEO List</v-toolbar-title>
              </v-toolbar>
              <v-data-table
                :headers="headers"
                :items="seos"
                :search="search"
                id="printMe"
              >
                <template v-slot:top>
                  <v-toolbar
                    flat
                  >
                    <v-toolbar-title>List</v-toolbar-title>
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
                    <nuxt-link to="/seo/addseo">
                      <v-btn
                            color="primary"
                            dark
                            class="mr-3 ml-3 font-weight-bold"
                            small
                          >
                            Add Seo
                      </v-btn>
                    </nuxt-link>
                    <v-btn icon :x-small="sizeXsm" :small="sizeSm" @click="print" class="mr-1 mr-lg-3">
                      <v-icon>{{mdiPrinter}}</v-icon>
                    </v-btn>
                  </v-toolbar>
                </template>
                <template v-slot:item.seos="{ item }">
                  <nuxt-link :to="{ name: 'seo-update-id', params: { id: item.id }}">
                    <v-icon
                      small
                      class="mr-2"
                    >
                      mdi-pencil
                    </v-icon>
                  </nuxt-link>
                  <!-- <nuxt-link to="#">
                      <v-icon
                        small
                        class="mr-2"
                      >
                        mdi-eye
                      </v-icon>
                  </nuxt-link> -->
                  <v-icon
                      @click="deleteSeo(item.id)"
                      color="#F44336">
                        mdi-trash-can
                  </v-icon>
                </template>
              </v-data-table>
            </v-card>
          </v-col>
           <!-- Delete Dialogue -->
          <v-dialog v-model="dialogDelete" max-width="500px">
            <v-card>
              <v-card-title class="text-h5">Are you sure you want to delete this item?</v-card-title>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="closeDelete">Cancel</v-btn>
                <v-btn color="blue darken-1" text @click="deleteConfirm">OK</v-btn>
                <v-spacer></v-spacer>
              </v-card-actions>
            </v-card>
          </v-dialog>
           <!-- End Delete Dialogue -->
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
            value: 'title',
            width: "15%",
            overflow: "hidden",
          },
          {
            text: 'Meta Title',
            value: 'meta_title',
            width: "10%",
            overflow: "hidden",
          },
          {
            text: 'Meta Description',
            value: 'meta_description',
            width: "20%",
            overflow: "hidden",
          },
          {
            text: 'Meta Keywords',
            value: 'meta_keywords',
            width: "10%",
            overflow: "hidden",
          },
          {
            text: 'Actions',
            value: 'seos',
            sortable: false,
            width: "10%",
            overflow: "hidden",
          },
        ],
      seos: [],
      mdiPrinter: mdiPrinter,
      dialogDelete: false,

    }),

    created () {

    },

    methods: {

      async getSeos() {
        try {
        const {data} = await this.$axios.get('/seos');
          this.seos = data;
        } catch (e) {
          this.error = e.data;
        }
      },

      deleteSeo(id){
        this.id = id,
        this.dialogDelete = true
      },

      deleteConfirm () {
        try {
          this.$axios.delete('/seos/'+this.id).then(
            this.getSeos(),
            this.closeDelete(),
            this.$router.push('/seo/seo')
          )
        } catch (e) {
          this.error = e.response
        }
      },

      closeDelete () {
        this.dialogDelete = false,
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      print () {
        // Pass the element id here
        this.$htmlToPaper('printMe');
      },

    },

    asyncData(context) {
      const AuthStr = 'Bearer '.concat(context.$auth.strategy.token.get());
      return context.$axios
        //.get(context.env.apiRoot + 'post-slug?slug=' + encodeURI(context.params.slug))
        .get('/seos', { headers: { Authorization: AuthStr } })
        .then((res) => {
          if (res.data.length === 0 || res.data.error) {
            throw({ statusCode: 404, message: 'Tags not found' })
          }
          // console.log(res.data);
          return { seos: res.data }
        })
        .catch(error => {
          if (error.response) {
            // Request made and server responded
            //this.errorResponse = error.response.data;
            this.errorCode = error.response.status;
          } else if (error.request) {
            // The request was made but no response was received
            //console.log(error.request);
          } else {
            // Something happened in setting up the request that triggered an Error
            return {error: error.message};
            return context.error({ statusCode: 500, message: error.message })
          }
        });
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
