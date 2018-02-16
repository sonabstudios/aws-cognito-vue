<template>
  <v-container grid-list-md class="mt-3">
    <v-layout row justify-space-around>

        <v-card class="main-card pa-4 ml-4 mr-4">
          <v-layout row wrap justify-space-around>

            <v-flex md1 class="hidden-sm-and-down">
            </v-flex>
            <v-flex md4 class="hidden-sm-and-down">
              <v-card class="elevation-0 pa-2">
                <v-card-media >
                <img class="aws-logo" src="../../static/aws_cognito.png">
                </v-card-media>
              </v-card>
            </v-flex>

            <v-flex md6>
              <v-card class="elevation-0 pa-2 ml-1 mr-1">
                <v-card-title primary-title>
                  <div>
                    <h4 class="headline mb-0">Register to AWS Cognito</h4>
                  </div>
                </v-card-title>
                <v-card-text>

                  <v-form v-model="valid">

                    <v-text-field
                      label="E-mail"
                      v-model="email"
                      :rules="emailRules"
                      required>
                    </v-text-field>

                    <v-text-field
                      label="Password"
                      v-model="password"
                      :rules="passRules"
                      :append-icon="hidepw ? 'visibility' : 'visibility_off'"
                      :append-icon-cb="() => (hidepw = !hidepw)"
                      :type="hidepw ? 'password' : 'text'"
                      required>
                    </v-text-field>

                  </v-form>

                  <v-btn
                    block
                    :loading="loading"
                    @click.native="onSubmit()"
                    :disabled="!valid"
                    class="mt-3 mb-3"
                    light
                    color="secondary">
                    Sign Up
                  </v-btn>
                  <div class="caption">
                    By signing up, you agree to the <router-link :to="''">Terms of Service</router-link> and <router-link :to="''">Privacy Policy</router-link>, including Cookie Use.
                  </div>
                </v-card-text>
              </v-card>
            </v-flex>
            <v-flex md1 class="hidden-sm-and-down">
            </v-flex>

         </v-layout>
        </v-card>

    </v-layout>
  </v-container>
</template>

<script>
import router from '../routes'

export default {
  data: () => ({
    valid: false,
    email: '',
    emailRules: [
      (v) => !!v || 'E-mail is required',
      // eslint-disable-next-line
      (v) => /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
    ],
    password: '',
    passRules: [
      (v) => !!v || 'Password is required',
      (v) => v.length >= 8 || 'Password must be 8-20 characters',
      (v) => /^(?=.*[0-9])/.test(v) || 'Password must contain at least 1 number',
      (v) => /^(?=.*[a-z])/.test(v) || 'Password must contain at least 1 lower case letter',
      (v) => /^(?=.*[A-Z])/.test(v) || 'Password must contain at least 1 upper case letter',
      (v) => /^(?=.*[!@#$%^&*"])/.test(v) || 'Password must contain at least 1 special character (!@#$%^&*")'
    ],
    hidepw: true,
    loader: false,
    loading: false
  }),
  methods: {
    onSubmit () {
      this.loader = 'loading'
      console.log('called')
      console.log(this.email)
      console.log(this.password)
      this.hide = !this.hide
    },
    navRreset: function () {
      router.push('/reset')
    }
  },
  watch: {
    loader () {
      const l = this.loader
      this[l] = !this[l]

      setTimeout(() => (this[l] = false), 3000)

      this.loader = null
    }
  }
}

</script>

<style scoped>
.aws-logo {
  width: 100%;
    height: 100%;
    object-fit: contain;
}

a {
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}
</style>