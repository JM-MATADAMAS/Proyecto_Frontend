<template>
  <div>
    <h1 class="fuente" style="display: flex; flex-direction: column; align-items: center; margin-bottom: 16px; margin-top: 10%; text-align: center; color: #4F4F4F;">
      Welcome, Log into your account
    </h1>
    <v-card
      elevation="0"
      color="#FFFFFF"
      style="display: flex; flex-direction: column; align-items: center; margin-top: 30px; width: 500px;  min-width: 500px;text-align: center;"
      class="mx-auto"
    >
      <v-card-subtitle color="#667085" style="font-size: 16px; margin-top: 8%; max-width: 55%; min-width: 50%;">
        It is our great pleasure to have you on board!
        <v-text-field
          v-model="schoolName"
          outlined
          dense
          single-line
          label="Enter the name of school"
          type="text"
          style="margin-top: 10%; font-size: small"
        />
        <v-text-field
          v-model="password"
          outlined
          dense
          single-line
          label="Enter password"
          type="password"
        />
        <v-btn block color="#2D88D4" elevation="0" style="color: white; padding: 0 0 0;" @click="login()">
          Login
        </v-btn>
      </v-card-subtitle>
      <v-card-subtitle style="padding: 0 0 50px 0;">
        Didn't already have an account?
        <a style="color: #2D88D4; text-decoration: none;" @click="SignUp ()">Sign up</a>
      </v-card-subtitle>
    </v-card>
  </div>
</template>

<script>
export default {
  name: 'LoginComponent',
  layout: 'login',
  data () {
    return {
      schoolName: null,
      password: null
    }
  },
  methods: {
    login () {
      const sendData = {
        nombreSchool: this.schoolName,
        password: this.password
      }
      // eslint-disable-next-line no-console
      console.log('@@ data =>', sendData)
      const url = 'http://localhost:8010/api/auth/login' // URL completa especificada aquí
      this.$axios.post(url, sendData)
        .then((res) => {
          // eslint-disable-next-line no-console
          console.log('@@ res =>', res)
          if (res.data.message === 'Logged In') {
            this.$nuxt.$emit('evento', {
              message: res.data.message,
              color: 'success',
              type: 'success',
              time: 2000
            })
            if (res.data.token) {
              localStorage.setItem('token', res.data.token)
              localStorage.setItem('nombreSchool', res.data.nombreSchool)
              // Redirigir a una página nueva
              this.$router.push('/principal')
            }
            this.$router.push({
              path: '/principal/'
            })
          }
        })
        .catch(() => {
          this.$nuxt.$emit('evento', {
            message: 'Something went wrong, try again',
            color: 'error',
            type: 'error',
            time: 2000
          })
        })
    },
    SignUp () {
      this.$router.push({
        path: '/signup/'
      })
    }
  }
}
</script>

<style>
/* Puedes añadir estilos adicionales aquí si es necesario */
</style>
