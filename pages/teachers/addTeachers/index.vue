<template>
  <div>
    <v-row style="font-weight: bold; margin-top: 1%; margin-left: 5%; margin-bottom:4% ;font-family: Kumbh Sans;">
      <v-spacer />
      <v-btn icon>
        <v-badge dot>
          <v-icon>
            mdi-bell-outline
          </v-icon>
        </v-badge>
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
          Add Teachers
          <v-spacer />
          <v-text-field
            v-model="designationTeacher"
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
          v-model="nameTeacher"
          label="Full name"
          outlined
          dense
        />
      </v-col>
      <v-row>
        <v-text-field
          v-model="emailTeacher"
          label="Email address"
          outlined
          dense
          style="margin-right: 1%; margin-left: 10%; margin-top: 1%; display: flex; font-family: Kumbh Sans; color: #4F4F4F;"
        />
        <v-col cols="4" style="display: flex; margin-left: 2%;  margin-right:20% ; font-family: Kumbh Sans; color: #4F4F4F;">
          <v-select
            v-model="classTeacher"
            outlined
            dense
            label="Class"
            :items="classItems"
            style="margin-right: 7%; width:auto;"
          />
          <v-select v-model="genderTeacher" outlined dense label="Gender" :items="genderItems" />
        </v-col>
      </v-row>
      <v-row>
        <v-text-field
          v-model="passwordTeacher"
          label="Password"
          outlined
          dense
          style=" margin-left: 10%; margin-top: 1%; display: flex; font-family: Kumbh Sans; color: #4F4F4F;"
        />
        <v-text-field
          v-model="phoneTeacher"
          label="Phone number"
          outlined
          dense
          style="margin-right: 18%; margin-left: 5%; margin-top: 1%; display: flex; font-family: Kumbh Sans; color: #4F4F4F;"
        />
      </v-row>
      <v-row>
        <v-col cols="2" style="margin-left: 9%;">
          <v-select v-model="subjectTeacher" label="Subject" dense outlined :items="subjectItems" />
        </v-col>
      </v-row>
      <v-row>
        <v-btn elevation="0" color="white" style="color:white; margin-left: 8%;">
          <v-icon color="#424242">
            mdi-plus-circle-outline
          </v-icon>
          <span style="color: #4F4F4F; text-transform: capitalize;" @click="addTeachers()">
            Add another
          </span>
        </v-btn>
        <v-btn elevation="0" color="#F1F1F1">
          <span style="color: #4F4F4F; text-transform: capitalize;" @click="addTeacher()">
            Add Teacher
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
      designationTeacher: null,
      nameTeacher: null,
      emailTeacher: null,
      classItems: ['S1', 'S2', 'C1', 'C2', 'E1', 'E2', 'A1', 'A2', 'G1', 'G2'],
      classTeacher: null,
      genderItems: ['Male', 'Female', 'Other'],
      genderTeacher: null,
      passwordTeacher: null,
      phoneTeacher: null,
      subjectItems: ['English', 'Spanish', 'Math', 'Art', 'Science', 'Physical Education', 'History'],
      subjectTeacher: null
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
      // eslint-disable-next-line no-console
      console.log(nombreSchool)
      if (nombreSchool) {
        this.designationTeacher = nombreSchool
      }
    },
    addTeacher () {
      const sendData = {
        designation: this.designationTeacher,
        fullName: this.nameTeacher,
        password: this.passwordTeacher,
        phoneNumber: this.phoneTeacher,
        subject: this.subjectTeacher,
        genero: this.genderTeacher,
        email: this.emailTeacher,
        id: Date.now().toString(),
        clase: this.classTeacher
      }
      // Verificar los datos antes de enviar
      // eslint-disable-next-line no-console
      console.log('@@ data =>', sendData)

      const url = 'http://localhost:8010/api/auth/signupTeacher/'
      this.$axios.post(url, sendData)
        .then((res) => {
          // eslint-disable-next-line no-console
          console.log('@@ res =>', res)
          if (res.data.message === 'Usuario Registrado Satisfactoriamente') {
            this.$router.push({
              path: '/teachers/allTeachers/'
            })
          }
        })
        .catch((err) => {
          // eslint-disable-next-line no-console
          console.log('@@ err =>', err.response ? err.response.data : err.message)
          this.$nuxt.$emit('evento', {
            message: err.response.data.message,
            color: 'error',
            type: 'error',
            time: 2000
          })
        })
    },
    addTeachers () {
      const sendData = {
        designation: this.designationTeacher,
        fullName: this.nameTeacher,
        password: this.passwordTeacher,
        phoneNumber: this.phoneTeacher,
        subject: this.subjectTeacher,
        genero: this.genderTeacher,
        email: this.emailTeacher,
        id: Date.now().toString(),
        clase: this.classTeacher
      }
      // Verificar los datos antes de enviar
      // eslint-disable-next-line no-console
      console.log('@@ data =>', sendData)

      const url = 'http://localhost:8010/api/auth/signupTeacher/'
      this.$axios.post(url, sendData)
        .then((res) => {
          // eslint-disable-next-line no-console
          console.log('@@ res =>', res)
          if (res.data.message === 'Usuario Registrado Satisfactoriamente') {
            this.$nuxt.$emit('evento', {
              message: res.data.message,
              color: 'success',
              type: 'success  ',
              time: 2000
            })
            this.nameTeacher = null
            this.emailTeacher = null
            this.classTeacher = null
            this.genderTeacher = null
            this.passwordTeacher = null
            this.phoneTeacher = null
            this.subjectTeacher = null
          }
        })
        .catch((err) => {
          // eslint-disable-next-line no-console
          console.log('@@ err =>', err.response ? err.response.data : err.message)
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
