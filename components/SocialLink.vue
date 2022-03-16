<template>
  <v-row dense>
    <v-col class="col-12">
      <v-card>
          <v-toolbar
            color="indigo font-weight-regular"
            dark
            dense
          >
          <v-toolbar-title>Social Media Link</v-toolbar-title>

          <v-spacer></v-spacer>
          </v-toolbar>
            <v-tabs
              v-model="tab"
            >
              <v-tab>
                <v-btn icon>
                  <v-icon>mdi-youtube</v-icon>
                </v-btn>
              </v-tab>
              <v-tab>
                <v-btn icon>
                  <v-icon>mdi-vimeo</v-icon>
                </v-btn>

              </v-tab>
              <v-tab>
                <v-btn icon>
                  <v-icon>mdi-facebook</v-icon>
                </v-btn>
              </v-tab>

              <v-tab>
                <v-btn icon>
                  <v-icon>mdi-twitter</v-icon>
                </v-btn>
              </v-tab>

              <v-tab>
                <v-btn icon>
                  <v-icon>mdi-instagram</v-icon>
                </v-btn>
              </v-tab>
            </v-tabs>

        <v-tabs-items v-model="tab">
          <v-tab-item>
            <v-card flat>
              <v-card-text>
                <v-text-field
                  ref="youtube_id"
                  v-model="youtube_id"
                  label="Youtube Id"
                  placeholder=""
                ></v-text-field>
              </v-card-text>
            </v-card>
          </v-tab-item>

          <v-tab-item>
            <v-card flat>
              <v-card-text>
              <v-text-field
                ref="vimeo_id"
                v-model="vimeo_id"
                label="Vimeo Link"
                placeholder=""
              ></v-text-field>
            </v-card-text>
            </v-card>
          </v-tab-item>

          <v-tab-item>
              <v-card flat>
              <v-card-text>
              <v-text-field
                ref="facebook_id"
                v-model="facebook_id"
                label="Facebook Link"
                placeholder=""
              ></v-text-field>
            </v-card-text>
            </v-card>
          </v-tab-item>

          <v-tab-item>
            <v-card flat>
              <v-card-text>
                <v-text-field
                  ref="twitter_id"
                  v-model="twitter_id"
                  label="Twitter Link"
                  placeholder=""
                ></v-text-field>
              </v-card-text>
            </v-card>
          </v-tab-item>

          <v-tab-item>
            <v-card flat>
              <v-card-text>
                <v-text-field
                  ref="instagram_id"
                  v-model="instagram_id"
                  label="Instagram Link"
                  placeholder=""
                ></v-text-field>
              </v-card-text>
            </v-card>
          </v-tab-item>

        </v-tabs-items>
      </v-card>
    </v-col>
  </v-row>
</template>
<script>
export default {
  data () {
    return {
      tab: null,
      youtube_id: null,
      vimeo_id: null,
      facebook_id: null,
      twitter_id: null,
      instagram_id: null,
    }
  },
  computed: {
    form () {
      return {
        youtube_id: this.youtube_id,
        vimeo_id: this.vimeo_id,
        facebook_id: this.facebook_id,
        twitter_id: this.twitter_id,
        instagram_id: this.instagram_id,
      }
    },
  },
}
</script>

