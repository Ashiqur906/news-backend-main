<template>
  <v-container>
    <v-row>
      <v-col class="col-12">
        <v-container fluid>
          <v-row dense>
            <v-col class="col-12">
              <v-card>
                <v-toolbar color="indigo" dark dense class="font-weight-bold">
                  <v-toolbar-title>Widgets List</v-toolbar-title>
                </v-toolbar>
                <!-- {{widgets}} -->
                <v-data-table
                  :headers="headers"
                  :items="widgets"
                  :search="search"
                  id="printMe"
                >
                  <template v-slot:top>
                    <v-toolbar flat>
                      <v-toolbar-title>List</v-toolbar-title>
                      <v-divider class="mx-4" inset vertical></v-divider>
                      <!-- <v-spacer></v-spacer> -->
                      <v-text-field
                        v-model="search"
                        append-icon="mdi-magnify"
                        label="Search"
                        single-line
                        hide-details
                      ></v-text-field>
                      <!-- <v-spacer></v-spacer> -->
                      <NuxtLink to="/widget/addWidget">
                        <v-btn
                          color="primary"
                          dark
                          class="mr-3 ml-3 font-weight-bold"
                          small
                        >
                          Add Widget
                        </v-btn>
                      </NuxtLink>
<!--                      <v-btn-->
<!--                        icon-->
<!--                        :x-small="sizeXsm"-->
<!--                        :small="sizeSm"-->
<!--                        @click="print"-->
<!--                        class="mr-1 mr-lg-3"-->
<!--                      >-->
<!--                        <v-icon>{{ mdiPrinter }}</v-icon>-->
<!--                      </v-btn>-->
                    </v-toolbar>
                  </template>
                  <template v-slot:item.status="{ item }">
                    <v-btn
                      x-small
                      color="primary"
                      dark
                      class="mb-2"
                      v-if="item.status == 1"
                    >
                      Active
                    </v-btn>
                    <v-btn x-small color="#F44336" dark class="mb-2" v-else>
                      Inactive
                    </v-btn>
                  </template>
                  <template v-slot:item.widgets="{ item }">
                    <!-- <nuxt-link :to="{ name: 'widget-view-id', params: { id: item.id }}">
                      <v-icon
                        small
                        class="mr-2"
                      >
                        mdi-eye
                      </v-icon>
                  </nuxt-link> -->
                    <!-- <nuxt-link :to="{ name: 'widget-update-id', params: { id: item.id }}">
                      <v-icon
                        small
                        class="mr-2"
                      >
                        mdi-pencil
                      </v-icon>
                  </nuxt-link>
                  <v-icon
                       @click="deletePost(item.id)"
                       color="#F44336">
                        mdi-trash-can
                  </v-icon> -->
                  </template>
                </v-data-table>
              </v-card>
            </v-col>
            <!-- Delete Dialogue -->
            <v-dialog v-model="dialogDelete" max-width="500px">
              <v-card>
                <v-card-title class="text-h5"
                  >Are you sure you want to delete this item?</v-card-title
                >
                <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn color="blue darken-1" text @click="closeDelete"
                    >Cancel</v-btn
                  >
                  <v-btn color="blue darken-1" text @click="deletePostConfirm"
                    >OK</v-btn
                  >
                  <v-spacer></v-spacer>
                </v-card-actions>
              </v-card>
            </v-dialog>
            <!-- End Delete Dialogue -->
          </v-row>
        </v-container>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    search: "",
    editLayout: "",
    headers: [
      {
        text: "Widgets Name",
        value: "name",
        align: "start",
        sortable: true,
        width: "25%",
      },
      // { text: "Path", value: "path", sortable: false, align: "start"},
      {
        text: "Type",
        value: "widget_type",
        sortable: true,
        align: "start",
        width: "25%",
      },
      // { text: "Data Limit", value: "data_limit", sortable: false, align: "center", width: "20%"},
      {
        text: "Status",
        value: "status",
        sortable: false,
        align: "center",
        width: "25%",
      },
      // { text: "Action", value: "widgets", sortable: false, align: "center", width: "25%"},
    ],
    editedItem: {
      image: "/assets/images/image-plus.png",
      name: "",
      url: "",
    },
    slug: "",
    selected_layout: "Default",
    widgets: [],
    dialogDelete: null,
    deletePostConfirm: null,
    closeDelete: null,
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New Item" : "Edit Item";
    },
  },

  watch: {
    dialog(val) {
      val || this.close();
    },
    dialogDelete(val) {
      val || this.closeDelete();
    },
  },

  created() {
    this.first();
  },

  methods: {
    initialize() {
      this.desserts = [];
    },

    imageShow(item, slug) {
      this.editLayout = slug;
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.editedItem.image = "/assets/images/layout-5.jpg";
      this.model = true;
    },
    first() {
      (this.editedItem.image = "/assets/images/layout-4.jpg"),
        (this.model = true);
    },
    status(item) {
      this.item = this.item.id(item);
    },
  },
  asyncData(context) {
    const AuthStr = "Bearer ".concat(context.$auth.strategy.token.get());
    return context.$axios
      .get("/widgets", {})
      .then((res) => {
        if (res.data.length === 0 || res.data.error) {
          throw {
            statusCode: 404,
            message: "widgets not found",
          };
        }
        // console.log(res.data.data);
        return {
          widgets: res.data.data,
        };
      })
      .catch((error) => {
        if (error.response) {
          // Request made and server responded
          //this.errorResponse = error.response.data;
          this.errorCode = error.response.status;
        } else if (error.request) {
          // The request was made but no response was received
          //console.log(error.request);
        } else {
          // Something happened in setting up the request that triggered an Error
          return {
            error: error.message,
          };
          return context.error({
            statusCode: 500,
            message: error.message,
          });
        }
      });
    },
};
</script>
