<template>
  <v-row class="text-center justify-center">
    <v-col cols="12" md="6" sm="8">
      <v-card class="mt-5" outlined>
        <v-card-title>
          <label class="text-center">Login</label>
        </v-card-title>
        <v-card-text>
          <v-form
            ref="form"
            method="post"
            @submit.prevent="login"
          >
            <v-text-field
              outlined
              prepend-inner-icon="mdi-email"
              placeholder="example@email.com"
              v-model="email"
              :rules="emailRules"
              label="  E-mail"
              required
            ></v-text-field>

            <v-text-field
              outlined
              label="Password"
              prepend-inner-icon="mdi-key"
              placeholder="password"
              type="password"
              v-model="password"
              :rules="passwordRules"
            ></v-text-field>

            <v-alert color="red" v-if="error" v-html="error"></v-alert>
            <v-btn
              color="success"
              class="mr-4"
              type="submit"
            >
              Login
            </v-btn>
          </v-form>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  auth: false,
  userLogin: '',
  valid: true,
  data() {
    return {
      email: '',
      password: '',
      error: null,

      passwordRules: [
        v => !!v || 'Password is required',
      ],

      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
    }
  },
  methods: {
    async login() {
      try {
        await this.$auth.loginWith('local', {
          data: {
            email: this.email,
            password: this.password
          }
        })

        this.$router.push('/layout/list')
      } catch (e) {
        this.error = e.response.data.message
      }
    }
  },
  asyncData(context) {
    if(context.$auth.loggedIn) {
      context.redirect(302, '/')
    }
  }
}
</script>

