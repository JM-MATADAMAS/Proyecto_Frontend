<template>
  <div>
    <v-row style="font-weight: bold; margin-top: 1%; margin-left: 5%; margin-bottom:4% ;font-family: Kumbh Sans;">
      <v-spacer />
      <v-btn icon>
        <v-icon>
          mdi-bell-outline
        </v-icon>
      </v-btn>
      <v-btn text style="color: white; font-family: Kumbh Sans; font-size: small; margin-right: 5%;" elevation="0" @click="logout()">
        <span style="color: #424242; text-transform: capitalize;">
          Log out
        </span>
      </v-btn>
    </v-row>
    <v-row />
    <v-card elevation="0">
      <v-col cols="8">
        <v-row style="margin-top: 9%; margin-left: 10%; font-family: Kumbh Sans; font-size: xx-large; color: #4F4F4F;">
          Add Students
          <v-spacer />
          <v-text-field
            v-model="designationStudent"
            label="Designation"
            outlined
            dense
            readonly
            disabled
          />
        </v-row>
        <v-row style="margin-left: 8%; font-family: Kumbh Sans; color: #4F4F4F;">
          <v-btn text style="color: white;">
            <span style="color: #424242; text-transform: capitalize; font-size: 18px;">
              Manualy
            </span>
          </v-btn>
          <v-btn text style="color: white; margin-left: 3%">
            <span style="color: #424242; text-transform: capitalize; font-size: 18px;">
              Import CSV
            </span>
          </v-btn>
        </v-row>
      </v-col>
      <v-col cols="8" style="margin-left: 8%; margin-top: 3%; font-family: Kumbh Sans; color: #4F4F4F;">
        <v-text-field
          v-model="nameStudent"
          label="Full name"
          outlined
          dense
        />
      </v-col>
      <v-row>
        <v-text-field
          v-model="emailStudent"
          label="Email address"
          outlined
          dense
          style="margin-right: 1%; margin-left: 10%; margin-top: 1%; display: flex; font-family: Kumbh Sans; color: #4F4F4F;"
        />
        <v-col cols="4" style="display: flex; margin-left: 2%;  margin-right:20% ; font-family: Kumbh Sans; color: #4F4F4F;">
          <v-select
            v-model="classStudent"
            outlined
            dense
            label="Class"
            :items="classItems"
            style="margin-right: 7%; width:auto;"
          />
          <v-select v-model="genderStudent" outlined dense label="Gender" :items="genderItems" />
        </v-col>
      </v-row>
      <v-row>
        <v-text-field
          v-model="passwordStudent"
          label="Password"
          outlined
          dense
          style=" margin-left: 10%; margin-top: 1%; display: flex; font-family: Kumbh Sans; color: #4F4F4F;"
        />
        <v-text-field
          v-model="phoneStudent"
          label="Phone number"
          outlined
          dense
          style="margin-right: 18%; margin-left: 5%; margin-top: 1%; display: flex; font-family: Kumbh Sans; color: #4F4F4F;"
        />
      </v-row>
      <v-row>
        <v-btn elevation="0" color="white" style="color:white; margin-left: 8%;">
          <v-icon color="#424242">
            mdi-plus-circle-outline
          </v-icon>
          <span style="color: #4F4F4F; text-transform: capitalize;" @click="addStudent()">
            Add another
          </span>
        </v-btn>
        <v-btn elevation="0" color="#F1F1F1">
          <span style="color: #4F4F4F; text-transform: capitalize;" @click="addStudentPush()">
            Add Student
          </span>
        </v-btn>
      </v-row>
    </v-card>
  </div>
</template>

<script>
export default {
  layout: 'principal',
  data: () => {
    return ({
      designationStudent: null,
      nameStudent: null,
      emailStudent: null,
      classItems: ['S1', 'S2', 'C1', 'C2', 'E1', 'E2', 'A1', 'A2', 'G1', 'G2'],
      classStudent: null,
      genderItems: ['Male', 'Female', 'Other'],
      genderStudent: null,
      passwordStudent: null,
      phoneStudent: null
    })
  },
  mounted () {
    this.getDesignation()
  },
  methods: {
    logout () {
      localStorage.removeItem('token', 'nombreSchool')
      this.$router.push({
        path: '/'
      })
    },
    getDesignation () {
      const nombreSchool = localStorage.getItem('nombreSchool')
      if (nombreSchool) {
        this.designationStudent = nombreSchool
      }
    },
    addStudentPush () {
      const sendData = {
        designation: this.designationStudent,
        fullName: this.nameStudent,
        password: this.passwordStudent,
        phoneNumber: this.phoneStudent,
        genero: this.genderStudent,
        email: this.emailStudent,
        id: Date.now().toString(),
        clase: this.classStudent
      }

      const url = 'http://localhost:8010/api/auth/signupStudents/'
      this.$axios.post(url, sendData)
        .then((res) => {
          if (res.data.message === 'Usuario Registrado Satisfactoriamente') {
            this.$router.push({
              path: '/students/allStudents/'
            })
          }
        })
        .catch((err) => {
          this.$nuxt.$emit('evento', {
            message: err.response.data.message,
            color: 'error',
            type: 'error',
            time: 2000
          })
        })
    },
    addStudent () {
      const sendData = {
        designation: this.designationStudent,
        fullName: this.nameStudent,
        password: this.passwordStudent,
        phoneNumber: this.phoneStudent,
        genero: this.genderStudent,
        email: this.emailStudent,
        id: Date.now().toString(),
        clase: this.classStudent
      }

      const url = 'http://localhost:8010/api/auth/signupStudents/'
      this.$axios.post(url, sendData)
        .then((res) => {
          if (res.data.message === 'Usuario Registrado Satisfactoriamente') {
            this.nameStudent = null
            this.passwordStudent = null
            this.phoneStudent = null
            this.genderStudent = null
            this.emailStudent = null
            this.classStudent = null
          }
        })
        .catch((err) => {
          this.$nuxt.$emit('evento', {
            message: err.response.data.message,
            color: 'error',
            type: 'error',
            time: 2000
          })
        })
    }
  }
}
</script>
