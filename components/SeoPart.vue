<template>
  <v-row dense>
    <v-col class="col-12">
      <v-card
        class="mx-auto"
      >
        <v-toolbar
          color="indigo font-weight-regular"
          dark
          dense
        >
          <v-toolbar-title>SEO Information</v-toolbar-title>
        </v-toolbar>
        <v-container fluid>
          <v-row dense>
            <v-col
              class="col-12"
            >
              <v-card ref="form">
                <v-card-text>
                  <v-text-field
                    ref="metaname"
                    v-model="metaname"
                    :rules="[() => !!metaname || 'Meta Title is required']"
                    :error-messages="errorMessages"
                    label="Meta Title"
                    placeholder=""
                    required
                  ></v-text-field>

                </v-card-text>
                <v-card-text>
                  <v-text-field
                    ref="metadescription"
                    v-model="metadescription"
                    label="Meta Description"
                  ></v-text-field>

                </v-card-text>
                <v-card-text>
                  <v-text-field
                    ref="metakeywords"
                    v-model="metakeywords"
                    label="Meta Keywords"
                  ></v-text-field>

                </v-card-text>
                <v-card-text>
                  <v-text-field
                    ref="canonicalurl"
                    v-model="canonicalurl"
                    label="Canonical URL"
                  ></v-text-field>

                </v-card-text>
                <v-card-text>
                  <v-text-field
                    ref="metatype"
                    v-model="metatype"
                    label="Meta Type"
                  ></v-text-field>

                </v-card-text>
                <v-card-text>
                  <v-text-field
                    ref="metaimage"
                    v-model="metaimage"
                    label="Meta Image link"
                  ></v-text-field>

                </v-card-text>
                <v-divider class="mt-12"></v-divider>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-col>
  </v-row>
</template>
<script>
export default {
  data: () => ({
    errorMessages: '',
    metaname: null,
    metadescription: null,
    metakeywords: null,
    canonicalurl: null,
    metatype: null,
    metaimage: null,
    formHasErrors: false,

  }),

  watch: {
    name () {
      this.errorMessages = ''
    },
  },
}
</script>
