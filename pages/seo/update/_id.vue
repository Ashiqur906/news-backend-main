<template>
  <v-row>
    <v-col>
      <!-- Seo Information -->
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
                <v-toolbar-title>Edit SEO</v-toolbar-title>
              </v-toolbar>
              <v-container fluid>
                <v-row dense>
                  <v-col
                    class="col-12"
                  >
                    <v-card ref="form">
                      <v-card-text>
                        <v-text-field
                          ref="title"
                          v-model="title"
                          :rules="[() => !!title || 'Title is required']"
                          :error-messages="errorMessages"
                          label="Title"
                          placeholder=""
                          required
                        ></v-text-field>

                      </v-card-text>
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
      <!-- Seo Information End -->
    </v-col>
  </v-row>
</template>
<script>
export default {
  data: () => ({
    errorMessages: '',
    statusCode: null,
    error: null,
  }),
  watch: {
    name () {
      this.errorMessages = ''
    },
  },
  
  methods: {
    submit () {
      try {
        this.$axios.put('/seos/'+ this.$route.params.id , {
          title: this.title,
          meta_title: this.meta_title,
          meta_description: this.meta_description,
          meta_keywords: this.meta_keywords,
          canonical_url: this.canonical_url,
          meta_type: this.meta_type,
          meta_image_link: this.meta_image_link,
        })

        this.$router.push('/seo/seo')
      } catch (e) {
        this.error = e.response.data.message
      }
    },
  },

  asyncData(context) {
    const AuthStr = 'Bearer '.concat(context.$auth.strategy.token.get());
    return context.$axios
      .get('/seos/' + context.params.id + '/edit', { headers: { Authorization: AuthStr } })
      .then((res) => {
        if (res.data.length === 0 || res.data.error) {
          throw({ statusCode: 404, message: 'Tag not found' })
        }
        return { seo: res.data, title: res.data.title, meta_title: res.data.meta_title, meta_description: res.data.meta_description, meta_keywords: res.data.meta_keywords, canonical_url: res.data.canonical_url, meta_type: res.data.meta_type, meta_image_link: res.data.meta_image_link }
      })
      .catch(error => {
        if (error.response) {
          // Request made and server responded
          this.errorCode = error.response.status;
        } else if (error.request) {
          // The request was made but no response was received
        } if (error.statusCode === 404) {
          return context.error({ statusCode: 404, message: error.message })
        } if (error.statusCode === 404) {
          return context.error({ statusCode: 404, message: error.message })
        }else {
          // Something happened in setting up the request that triggered an Error
          return {error: error.message};
          return context.error({ statusCode: 500, message: error.message })
        }
      });
  },

}
</script>
