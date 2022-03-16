<template>
  <v-row class="text-center justify-center">
    <v-col cols="12" md="6" sm="8">
      <v-card class="mt-5" outlined>

        <v-card-title>
          <label class="text-center">Register</label>
        </v-card-title>
        <v-card-text>
          <v-form
            ref="form"
            method="post"
            @submit.prevent="register"
          >
            <v-text-field
              label="Name"
              :rules="rules"
              v-model="name"
              hide-details="auto"
            ></v-text-field>
            <br>
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
              v-model="password"
              label="Password"
              name="password"
              prepend-icon="mdi-lock"
              type="password"
              :rules="passwordRules"
            />

            <v-text-field
              v-model="confirmPassword"
              label="Confirm Password"
              name="confirmPassword"
              prepend-icon="mdi-lock"
              type="password"
              :rules="confirmPasswordRules"
            />

            <v-btn
              color="success"
              class="mr-4"
              type="submit"
            >
              Register
            </v-btn>
          </v-form>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>


<script>


export default {
  auth:false,
  userLogin: '',
  valid: true,
  data() {
    return {
      email: null,
      name: null,
      error: null,
      rules: [
        value => !!value || 'Required.',
        value => (value && value.length >= 3) || 'Min 3 characters',
      ],
      password: '',
      confirmPassword: '',
      passwordRules: [
        (value) => !!value || 'Please type password.',
        (value) => (value && value.length >= 6) || 'minimum 6 characters',
      ],
      confirmPasswordRules: [
        (value) => !!value || 'type confirm password',
        (value) =>
          value === this.password || 'The password confirmation does not match.',
      ],

      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
    }
  },
  methods: {
    async register() {
      try {
        await this.$axios.post('http://127.0.0.1:8000/api/register', {
          name: this.name,
          email: this.email,
          password: this.password,
          confirm_password: this.confirmPassword
        })

        await this.$auth.loginWith('local', {
          data: {
            email: this.email,
            password: this.password
          },
        })

        this.$router.push('/')
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

