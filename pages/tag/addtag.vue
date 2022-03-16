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
            <v-toolbar-title>Tag Information</v-toolbar-title>


          </v-toolbar>

          <v-container fluid>
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
                      @keyup="makeSlug()"
                      placeholder=""
                      required
                    ></v-text-field>
                    <v-text-field
                      label="Slug"
                      name="slug"
                      v-model="slug"
                      required
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
    </v-col>
    <!-- Right Side -->
    <v-col class="col-4">

      <!-- Published Type -->
      <v-container fluid>
        <v-row dense>
          <v-col class="col-12">

      <v-card class="mx-auto">
        <v-toolbar
            color="indigo"
            class="font-weight-regular"
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
                  :label="status ? 'Tag Active' : 'Tag Deactive'"
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
      <!-- Seo Information -->
      <v-container fluid>
        <SeoPart/>
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
    slug: "",
    formHasErrors: false,
    status: true,
  }),

  watch: {
    name () {
      this.errorMessages = ''
    },
  },
  mounted(e) {
    this.slug = this.makeSlug()
  },

  methods: {
    submit () {
      if (this.title.length && this.slug.length !== 0) {
        try {
          
          this.$axios.post('/tags', {
            title: this.title,
            slug: this.slug,
            status: this.status?1:0,
            
          })
          
          this.$router.push('/tag/tag')
        } catch (e) {
          this.error = e.response.data.message
        }
      } else {
        alert('Please fill the required Fields')
      }
      
    },
    makeSlug(){
      this.slug = this.title.trim().toLowerCase().replaceAll(' ','-');
    },

  },
}
</script>
