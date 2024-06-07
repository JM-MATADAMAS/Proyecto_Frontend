<template>
  <div>
    <h1 class="fuente title-text">
      Welcome, Log into your account
    </h1>
    <v-card
      elevation="0"
      color="#FFFFFF"
      class="login-card"
    >
      <v-card-subtitle class="card-subtitle">
        It is our great pleasure to have you on board!
        <v-text-field
          v-model="schoolName"
          outlined
          dense
          single-line
          label="Enter the name of school"
          type="text"
          class="input-field"
        />
        <v-text-field
          v-model="password"
          outlined
          dense
          single-line
          label="Enter password"
          type="password"
        />
        <v-btn
          block
          color="#2D88D4"
          elevation="0"
          class="login-btn"
          style="color: white;"
          @click="login()"
        >
          Login
        </v-btn>
      </v-card-subtitle>
      <v-card-subtitle class="signup-subtitle">
        Didn't already have an account?
        <a class="signup-link" @click="SignUp()">Sign up</a>
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
.title-text {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 16px;
  margin-top: 10%;
  text-align: center;
  color: #4F4F4F;
}

.login-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 30px;
  width: 30%;
  min-width: 300px;
  max-width: 90%;
  text-align: center;
  margin-left: auto;
  margin-right: auto;
}

.card-subtitle {
  color: #667085;
  font-size: 16px;
  margin-top: 8%;
  margin-bottom: 2%;
  max-width: 90%;
  min-width: 50%;
}

.input-field {
  margin-top: 15%;
  font-size: small;
}

.login-btn {
  color: white;
  padding: 0 0 0;
}

.signup-subtitle {
  padding: 0 0 50px 0;
}

.signup-link {
  color: #2D88D4;
  text-decoration: none;
}

@media (max-width: 600px) {
  .title-text {
    margin-top: 20%;
    font-size: 18px;
  }

  .login-card {
    width: 90%;
    min-width: 90%;
  }

  .card-subtitle {
    font-size: 14px;
  }

  .input-field {
    margin-top: 5%;
  }
}
</style>
