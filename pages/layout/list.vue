<template>
  <v-container>
    <v-row>
      <v-col cols="12" md="5" sm="5" class="">
        <v-card style="border-radius: 5px">
          <!-- {{layouts}} -->
          <v-data-table
            :headers="headers"
            :items="layouts"
            :search="search"
            :items-per-page="6"
            sort-by="calories"
            class="elevation-1"
            style="font-size: 20px"
          >
            <template v-slot:item.image="{ item }">
              <v-container class="content-center" align="center">
                <v-img
                  :lazy-src="item.image"
                  min-height="50"
                  max-height="150"
                  min-width="50"
                  max-width="150"
                  :src="'/assets/images/layout-4.jpg'"
                  :alt="item.name"
                  @click="imageShow(item, item.path)"
                ></v-img>
                <v-chip class="mt-1" color="#00954c">
                  {{ item.title }}
                </v-chip>
              </v-container>
            </template>

            <template v-slot:item.status="{ item }">
              <v-switch
                :key="item.path"
                v-model="item.path"
                :label="item.status === 1 ? 'Active' : 'Inactive'"
                :value="item.status === 0 ? 1 : 0"
                @change="setActive(item.path)"
                v-if="item.status === 1"
                disabled
              ></v-switch>
              <v-switch
                v-else
                :key="item.path"
                :v-model="path"
                :label="item.status === 1 ? 'Active' : 'Inactive'"
                @change="setActive(item.path)"
              ></v-switch>
            </template>
            <template v-slot:item.layouts="{ item }">
              <nuxt-link
                :to="{ name: 'layout-view-id', params: { id: item.id }}">
                <v-icon
                  small
                  class="mr-2"
                  v-if="item.path==='theme-default'"
                >
                  mdi-trash
                </v-icon>
                <v-icon
                  small
                  class="mr-2"
                  v-else
                >
                  mdi-pencil
                </v-icon>
              </nuxt-link>
            </template>
          </v-data-table>
        </v-card>
      </v-col>
      <v-col cols="12" md="7" sm="7" class="text-center">
        <v-card v-if="model != null" style="border-radius: 5px">
          <v-card-title>
            Layout Preview
          </v-card-title>
        </v-card>
        <v-card v-if="model != null" style="border-radius: 5px">
          <!-- {{ editLayout }} -->
          <v-img
            :src="editedItem.image"
            class="image-preview"
            aspect-ratio="1.6"
          ></v-img>
        </v-card>
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
        text: "Layouts",
        value: "image",
        align: "start",
        sortable: false,
      },
      {
        text: "Actions",
        value: "status",
        sortable: false,
        align: "left",
      },
      {
        text: "Modify",
        value: "layouts",
        sortable: false,
        align: "center",
      },
    ],
    editedItem: {
      image: "/assets/images/image-plus.png",
      name: "",
      url: "",
    },
    path: "",
    selected_layout: "Default",
    layouts: [],
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New Item" : "Edit Item";
    },

    localAttrs() {
      const attrs = {};

      if (this.variant === "default") {
        attrs.absolute = false;
        attrs.fixed = false;
      } else {
        attrs[this.variant] = true;
      }
      return attrs;
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
    this.initialize();
    this.first();
  },

  methods: {
    initialize() {
      this.desserts = [
        {
          name: "Layout 1",
          path: "nature-image",
          image: "/assets/images/Layout One.jpg",
          uploaded: "13-Oct-2021",
        },
        {
          name: "Layout 2",
          path: "nature-image",
          image: "/assets/images/Layout Two.jpg",
          uploaded: "13-Oct-2021",
        },
        {
          name: "Layout 3",
          path: "nature-image",
          image: "/assets/images/Layout Three.jpeg",
          uploaded: "13-Oct-2021",
        },
        {
          name: "Layout 4",
          path: "nature-image",
          image: "/assets/images/layout-4.jpg",
          uploaded: "13-Oct-2021",
        },
        {
          name: "Layout",
          path: "nature-image",
          image: "/assets/images/layout-5.jpg",
          uploaded: "13-Oct-2021",
        },
      ];
    },

    imageShow(item, path) {
      this.editLayout = path;
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

    // Active Layout
    setActive(path) {
      try {
        this.$axios.get("layout/status/" + path);
        this.$nuxt.refresh();
      } catch (e) {
        this.error = e.response.data.message;
      }
    },
  },
  asyncData(context) {
    const AuthStr = "Bearer ".concat(context.$auth.strategy.token.get());
    return (
      context.$axios
        //.get(context.env.apiRoot + 'post-path?path=' + encodeURI(context.params.path))
        .get("/layouts", {
          headers: {
            Authorization: AuthStr,
          },
        })
        .then((res) => {
          if (res.data.length === 0 || res.data.error) {
            throw {
              statusCode: 404,
              message: "Posts not found",
            };
          }
          // console.log(res.data.data);
          return {layouts: res.data.data};
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
        })
    );
  },
};
</script>
