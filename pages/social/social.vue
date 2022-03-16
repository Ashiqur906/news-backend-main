<template>
  <v-row>
    <v-col class="col-12">
      <v-container fluid>
        <v-row dense>
          <v-col class="col-12">
            <v-card>
              <v-toolbar
                class="font-weight-bold"
                color="indigo"
                dark
                dense
              >
                <v-toolbar-title>Social link List</v-toolbar-title>
              </v-toolbar>

              <v-data-table
                :headers="headers"
                :items="socials"
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
                  <nuxt-link to="/social/addSocial">
                    <v-btn
                          color="primary font-weight-bold"
                          dark
                          class="ml-3 mr-3"
                          small
                        >
                          Add Socials Link
                    </v-btn>
                  </nuxt-link>
                  <v-btn icon :x-small="sizeXsm" :small="sizeSm" @click="print" class="mr-1 mr-lg-3">
                    <v-icon>{{mdiPrinter}}</v-icon>
                  </v-btn>
                </v-toolbar>
              </template>
              <template v-slot:item.logo="{item}">
                <v-img
                  :lazy-src="item.logo"
                  min-height="50"
                  max-height="150"
                  style="margin:5px; border-radius:10px;"
                  min-width="50"
                  max-width="150"
                  :src="item.logo"
                  :alt="item.title"
                ></v-img>
              </template>

              <template v-slot:item.socials="{ item }">
                <nuxt-link :to="{ name: 'social-update-id', params: { id: item.id }}">
                  <v-icon
                    small
                    class="mr-2"
                  >
                    mdi-pencil
                  </v-icon>
                </nuxt-link>
                <v-icon
                  @click="deleteSocial(item.id)"
                  color="#F44336"
                  >
                    mdi-trash-can
                </v-icon>
              </template>
              <template v-slot:item.isActive="{ item }">
                <v-btn
                  x-small
                  color="primary"
                  dark
                  class="mb-2"
                  v-if="item.isActive==1"
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

              </v-data-table>

            </v-card>
          </v-col>
          <!-- Delete Dialogue -->
          <v-dialog v-model="dialogDeleteSocial" max-width="500px">
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
        dialogDelete: false,
        headers: [
          {
            text: 'Title',
            align: 'start',
            sortable: true,
            value: 'title',
            width: "15%",
            overflow: "hidden",
          },
          {
            text: 'Logo',
            align: 'start',
            sortable: true,
            value: 'logo',
            width: "15%",
            overflow: "hidden",
          },
          {
            text: 'Url',
            align: 'start',
            sortable: true,
            value: 'url',
            width: "15%",
            overflow: "hidden",
          },
          {
            text: 'Status',
            value: 'isActive',
            width: "10%",
            overflow: "hidden",
          },
          {
            align:'center',
            text: 'Actions',
            value: 'socials',
            sortable: false,
            width: "10%",
            overflow: "hidden",
          },
        ],
      socials: [],
      mdiPrinter: mdiPrinter,
      dialogDeleteSocial: '',

    }),
    created () {
      // this.initialize()
    },

    methods: {

      print () {
        // Pass the element id here
        this.$htmlToPaper('printMe');
      },

      async getSocial() {
        try {
          const {data} = await this.$axios.get('/socials');
          this.socials = data.data;
        } catch (e) {
          this.error = e.data;
        }
      },

      deleteSocial(id){
        this.id = id,
        this.dialogDeleteSocial = true
      },

      deleteConfirm () {
        try {
          this.$axios.delete('/socials/'+this.id).then(

          ),
          this.closeDelete(),
          this.$router.push('/social/social')
        } catch (e) {
          this.error = e.response
        }
      },

      closeDelete () {
        this.dialogDeleteSocial = false,
        this.getSocial(),
        this.$nextTick(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },
    },

    asyncData(context) {
      const AuthStr = 'Bearer '.concat(context.$auth.strategy.token.get());
      return context.$axios
        //.get(context.env.apiRoot + 'post-slug?slug=' + encodeURI(context.params.slug))
        .get('/socials', { headers: { Authorization: AuthStr } })
        .then((res) => {
          if (res.data.length === 0 || res.data.error) {
            throw({ statusCode: 404, message: 'Social Link not found' })
          }
          // console.log(res.data);
          return { socials: res.data.data }
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
