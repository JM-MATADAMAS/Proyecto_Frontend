<template>
  <div class="main-container">
    <!--Cabecera de la página-->
    <h1 class="fuente header-text">
      Welcome, create your school account
    </h1>
    <v-card
      elevation="0"
      color="#FFFFFF"
      class="mx-auto responsive-card"
    >
      <v-card-subtitle class="subtitle-text">
        It is our great pleasure to have you on board!
        <!--Menú donde se solicita correo, administrador y escuela-->
        <div v-if="!showPasswordFields && !showStaffFields">
          <v-text-field
            v-model="adminName"
            :rules="name"
            outlined
            dense
            single-line
            label="Enter the name of admin"
            type="text"
            class="input-field"
          />
          <v-text-field
            v-model="schoolName"
            :rules="required"
            outlined
            dense
            single-line
            label="Enter the name of school"
            type="text"
          />
          <v-text-field
            v-model="schoolEmail"
            :rules="correo"
            outlined
            dense
            single-line
            label="Enter the school email"
            type="text"
          />
          <v-btn block color="#2D88D4" elevation="0" class="next-button" @click="goToPasswordFields">
            Next
          </v-btn>
        </div>
        <!--Menú donde se solicita la contraseña y si son iguales-->
        <div v-if="showPasswordFields && !showStaffFields" class="password-fields">
          <v-text-field
            v-model="password"
            :rules="passwords"
            :type="passwordFieldType"
            outlined
            dense
            single-line
            label="Choose a password"
            :append-icon="passwordFieldType === 'password' ? 'mdi-eye-off-outline' : 'mdi-eye-outline'"
            class="input-field"
            @click:append="togglePasswordVisibility"
          />
          <v-text-field
            v-model="passwordConfirm"
            :rules="passwords"
            :type="confirmPasswordFieldType"
            outlined
            dense
            single-line
            label="Confirm password"
            :append-icon="confirmPasswordFieldType === 'password' ? 'mdi-eye-off-outline' : 'mdi-eye-outline'"
            @click:append="toggleConfirmPasswordVisibility"
          />
          Must be at least 8 characters.
          <v-btn
            block
            color="#2D88D4"
            elevation="0"
            class="next-button"
            @click="goToStaffFields"
          >
            Next
          </v-btn>
        </div>
        <!--Menú donde se ingresar a los colaboradores-->
        <div v-if="showStaffFields">
          <v-select v-model="staffNumber" :items="staffItems" class="input-field" outlined label="staff" />
          <v-select v-model="schoolAddress" :items="schoolItems" outlined label="School address" />
          <v-btn block color="#2D88D4" elevation="0" class="next-button" @click="completeSignup">
            Next
          </v-btn>
        </div>
      </v-card-subtitle>
      <v-card-subtitle class="subtitle-bottom">
        <div v-if="!showPasswordFields && !showStaffFields">
          Already have an account?
          <a style="color: #2D88D4; text-decoration: none;" @click="Login">Login</a>
        </div>
      </v-card-subtitle>
    </v-card>
    <v-stepper v-if="showPasswordFields || showStaffFields" alt-labels elevation="0" class="stepper-custom">
      <v-stepper-header>
        <v-stepper-step step="1" style="font-size: small;" :complete="step > 1">
          Your details
          <small>Name and email</small>
        </v-stepper-step>

        <v-divider />

        <v-stepper-step step="2" style="font-size: small;" :complete="step > 2">
          Choose a password
          <small>Choose a secure password</small>
        </v-stepper-step>

        <v-divider />

        <v-stepper-step step="3" style="font-size: small;" :complete="step > 3">
          Invite your team
          <small>Start Collaborating</small>
        </v-stepper-step>

        <v-divider />

        <v-stepper-step step="4" style="font-size: small;" :complete="step > 4">
          Upload school's document
          <small>For account verification</small>
        </v-stepper-step>
      </v-stepper-header>
    </v-stepper>
  </div>
</template>

<script>
export default {
  name: 'SignupPage',
  layout: 'login',
  data () {
    return {
      step: 1,
      adminName: null,
      schoolName: null,
      schoolEmail: null,
      password: null,
      passwordConfirm: null,
      staffItems: ['Admin', 'Secretaria', 'Recursos Humanos', 'Becas', 'Psicología', 'Deportes', 'Biblioteca', 'Laboratorio'],
      staffNumber: null,
      schoolItems: ['Avenida Universidad No. 789, Colonia El Refugio', 'Boulevard del Sol No. 2345, Colonia La Esperanza', 'Calle Independencia No. 456, Colonia Las Rosas', 'Avenida Revolución No. 678, Colonia San Ángel', 'Calle de los Pinos No. 123, Colonia Centro'],
      schoolAddress: null,
      showPasswordFields: false,
      showStaffFields: false,
      passwordFieldType: 'password',
      confirmPasswordFieldType: 'password',
      required: [
        (value) => {
          if (value?.length > 0) {
            return true
          }
          return 'Rellena el campo obligatorio.'
        }
      ],
      passwords: [
        (value) => {
          if (value?.length > 7) { return true }
        }
      ],
      name: [
        (value) => {
          const nameRegex = /^[a-zA-ZáéíóúÁÉÍÓÚñÑ\s]+$/
          if (value?.length > 0 && nameRegex.test(value)) {
            return true
          }
          return 'El nombre solo puede contener letras y espacios.'
        }
      ],
      correo: [
        v => (/.+@.+\..+/.test(v) ? true : 'Ingresa un correo válido')
      ]
    }
  },
  methods: {
    Login () {
      this.$router.push({
        path: '/login/'
      })
    },
    togglePasswordVisibility () {
      this.passwordFieldType = this.passwordFieldType === 'password' ? 'text' : 'password'
    },
    toggleConfirmPasswordVisibility () {
      this.confirmPasswordFieldType = this.confirmPasswordFieldType === 'password' ? 'text' : 'password'
    },
    goToPasswordFields () {
      const nameRegex = /^[a-zA-ZáéíóúÁÉÍÓÚñÑ\s]+$/
      const emailRegex = /.+@.+\..+/

      const isAdminValid = this.adminName?.length > 0 && nameRegex.test(this.adminName)
      const isSchoolValid = this.schoolName?.length > 0
      const isSchoolEmailValid = emailRegex.test(this.schoolEmail)

      if (isAdminValid && isSchoolValid && isSchoolEmailValid) {
        this.showPasswordFields = true
        this.step = 2
      } else {
        if (!isAdminValid) {
          this.$nuxt.$emit('evento', {
            message: 'Algo salió mal',
            color: 'error',
            type: 'error'
          })
        }
        if (!isSchoolValid) {
          this.$nuxt.$emit('evento', {
            message: 'Algo salió mal',
            color: 'error',
            type: 'error'
          })
        }
        if (!isSchoolEmailValid) {
          this.$nuxt.$emit('evento', {
            message: 'Algo salió mal',
            color: 'error',
            type: 'error'
          })
        }
      }
    },
    goToStaffFields () {
      const Password = this.password
      const PasswordConfirm = this.passwordConfirm
      if ((Password === PasswordConfirm) && (Password !== null) && (Password.length > 7)) {
        this.showPasswordFields = false
        this.showStaffFields = true
        this.step = 3
      } else {
        this.$nuxt.$emit('evento', {
          message: 'Algo salió mal',
          color: 'error',
          type: 'error'
        })
      }
    },
    completeSignup () {
      this.step = 4
      // Lógica adicional para completar el registro
      const sendData = {
        id: Date.now().toString(),
        email: this.schoolEmail,
        password: this.password,
        nombreAdmin: this.adminName,
        nombreSchool: this.schoolName,
        numeroStaff: this.staffNumber,
        directionSchool: this.schoolAddress
      }
      // eslint-disable-next-line no-console
      console.log('@@ data =>', sendData)
      const url = 'http://localhost:8010/api/auth/signup' // URL completa especificada aquí
      this.$axios.post(url, sendData)
        .then((res) => {
          // eslint-disable-next-line no-console
          console.log('@@ res =>', res)
          if (res.data.message === 'Usuario Registrado Satisfactoriamente') {
            this.$nuxt.$emit('evento', {
              message: res.data.message,
              color: 'success',
              type: 'success',
              time: 2000
            })
            this.$router.push({ path: '/login/' })
          }
        })
        .catch((err) => {
          // eslint-disable-next-line no-console
          console.log('@@ err =>', err)
        })
    }

  }
}
</script>

<style scoped>
.main-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 16px;
  box-sizing: border-box;
}

.header-text {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 16px;
  margin-top: 4%;
  text-align: center;
  color: #4F4F4F;
}

.responsive-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 30px;
  width: 90%;
  max-width: 500px;
  min-width: 300px;
  text-align: center;
}

.subtitle-text {
  font-size: 16px;
  margin-top: 12%;
  max-width: 55%;
  min-width: 50%;
}

.subtitle-bottom {
  padding: 0 0 50px 0;
}

.input-field {
  margin-top: 10%;
}

.next-button {
  color: white;
  padding: 0 0 0;
}

.password-fields {
  font-size: small;
}

@media (min-width: 600px) {
  .responsive-card {
    width: 500px;
    min-width: 500px;
  }
}

.stepper-custom {
  color: #f3f3f3;
  position: fixed;
  bottom: 0;
  width: 100%;
}

.stepper-custom .v-stepper__step {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  align-items: center;
}

.stepper-custom .v-stepper__step small {
  display: block;
  width: 100%;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>
