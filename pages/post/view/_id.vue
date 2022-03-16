<template>

  <v-card>
    <v-toolbar
      color="indigo"
      dark
      dense
      class="font-weight-bold"
    >
      <v-toolbar-title >Post View</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        x-small
        color="primary"
        dark
        class="mb-2"
        v-if="status==1"
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
    </v-toolbar>
    <v-simple-table>

      <template v-slot:default>

        <thead>
        <tr>
          <th class="text-left">
            Heading
          </th>
          <th class="text-left">
            Designation
          </th>
        </tr>
        </thead>
        <tbody>
        <tr>
          <td width="20%">Title</td>
          <td class="py-4">{{title}}</td>
        </tr>
        <tr>
          <td width="20%">Short Description</td>
          <td class="py-8" v-html="short_description"></td>
        </tr>
        <tr>
          <td width="20%">Description</td>
          <td class="py-8" v-html="description"></td>
        </tr>
        <tr>
          <td width="20%">Image</td>
          <td class="py-8">
<!--            {{posts['pictures']?posts[0]['pictures'][0]['thumbnail']:''}}-->
<!--            {{pictures[0]['thumbnail']}}-->
            <v-img

              min-height="50"
              max-height="150"
              style="margin:5px;
                    border-radius:10px;"
              min-width="50"
              max-width="150"
              :src="pictures[0]?pictures[0]['thumbnail']: ''"
              alt="No Image"
            ></v-img>
          </td>
        </tr>
        <tr>
          <td width="20%">Categories</td>
          <td class="py-8">
            <span v-for="category in categories">
              <span>
                {{category.title}},
              </span>
            </span>
          </td>
        </tr>
        </tbody>
      </template>
    </v-simple-table>
  </v-card>

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
    short_description: "",
    description: "",
    pictures: ""

  }),


  methods: {


  },

  asyncData(context) {
    const AuthStr = 'Bearer '.concat(context.$auth.strategy.token.get());
    return context.$axios
      .get('/posts/' + context.params.id + '/edit', { headers: { Authorization: AuthStr } })
      .then((res) => {
        if (res.data.length === 0 || res.data.error) {
          throw({ statusCode: 404, message: 'Post not found' })
        }
        return { categories: res.data.categories, post: res.data, title: res.data.post.title,
        slug: res.data.post.slug, description: res.data.post.description, status: res.data.post.status,
        short_description: res.data.post.short_description, pictures: res.data.post.pictures, category_id: res.data.categories.category_id }
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
