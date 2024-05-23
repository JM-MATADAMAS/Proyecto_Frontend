<template>
  <div>
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
        <div v-if="!showPasswordFields">
          <v-text-field
            outlined
            dense
            single-line
            label="Enter the name of admin"
            type="text"
            style="margin-top: 10%;"
          />
          <v-text-field outlined dense single-line label="Enter the name of school" type="text" />
          <v-text-field outlined dense single-line label="Enter the school email" type="text" />
          <v-btn block color="#2D88D4" elevation="0" style="color: white; padding: 0 0 0;" @click="goToPasswordFields">
            Next
          </v-btn>
        </div>
        <div v-if="showPasswordFields && !showStaffFields">
          <v-text-field
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
            :type="confirmPasswordFieldType"
            outlined
            dense
            single-line
            label="Confirm password"
            :append-icon="confirmPasswordFieldType === 'password' ? 'mdi-eye-off-outline' : 'mdi-eye-outline'"
            @click:append="toggleConfirmPasswordVisibility"
          />
          <v-btn block color="#2D88D4" elevation="0" style="color: white; padding: 0 0 0;" @click="goToStaffFields">
            Next
          </v-btn>
        </div>
        <div v-if="showStaffFields">
          <v-select style="margin-top: 10%;" outlined label="Number of staff" />
          <v-select outlined label="School address" />
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
      showPasswordFields: false,
      showStaffFields: false,
      passwordFieldType: 'password',
      confirmPasswordFieldType: 'password'
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
      this.showPasswordFields = true
      this.step = 2
    },
    goToStaffFields () {
      this.showStaffFields = true
      this.step = 3
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
