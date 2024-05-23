<template>
  <div>
    <!--Cabecera de la página-->
    <h1 class="fuente" style="display: flex; flex-direction: column; align-items: center; margin-bottom: 16px; margin-top: 4%; text-align: center; color: #4F4F4F;">
      Welcome, create your school account
    </h1>
    <v-card
      elevation="0"
      color="#FFFFFF"
      style="display: flex; flex-direction: column; align-items: center; margin-top: 30px; width: 500px;  min-width: 500px;text-align: center;"
      class="mx-auto"
    >
      <v-card-subtitle color="#667085" style="font-size: 16px; margin-top: 12%; max-width: 55%; min-width: 50%;">
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
            style="margin-top: 10%;"
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
          <v-btn block color="#2D88D4" elevation="0" style="color: white; padding: 0 0 0;" @click="goToPasswordFields">
            Next
          </v-btn>
        </div>
        <!--Menú donde se solicita la contraseña y si son iguales-->
        <div v-if="showPasswordFields && !showStaffFields" style="font-size: small;">
          <v-text-field
            v-model="password"
            :rules="passwords"
            :type="passwordFieldType"
            outlined
            dense
            single-line
            label="Choose a password"
            :append-icon="passwordFieldType === 'password' ? 'mdi-eye-off-outline' : 'mdi-eye-outline'"
            style="margin-top: 10%;"
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
            style="color: white; padding: 0 0 0;"
            @click="goToStaffFields"
          >
            Next
          </v-btn>
        </div>
        <!--Menú donde se ingresar a los colaboradores-->
        <div v-if="showStaffFields">
          <v-select v-model="staffNumber" style="margin-top: 10%;" outlined label="Number of staff" />
          <v-select v-model="schoolAddress" outlined label="School address" />
          <v-btn block color="#2D88D4" elevation="0" style="color: white; padding: 0 0 0;" @click="completeSignup">
            Next
          </v-btn>
        </div>
      </v-card-subtitle>
      <v-card-subtitle style="padding: 0 0 50px 0;">
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
      staffNumber: null,
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
    }
  }
}
</script>

<style scoped>
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
