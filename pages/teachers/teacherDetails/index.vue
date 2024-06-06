<template>
  <div>
    <v-row style="margin-top: 1%; margin-left: 5%;">
      <v-btn text style="color: white; font-family: Kumbh Sans; font-size: small; margin-right: 2.7%;" elevation="0">
        <span style="color: #2671B1; text-transform: capitalize;">
          Export CSV
        </span>
      </v-btn>
      <v-btn color="#509CDB" style="color: white; font-family: Kumbh Sans; font-size: small; margin-right: 5%;" elevation="0" @click="$router.push({ path: '/teachers/addTeachers'})">
        <span style="color: #ffffff; text-transform: capitalize;">
          Add Teachers
        </span>
      </v-btn>
      <v-spacer />
      <v-btn icon>
        <v-icon>
          mdi-bell-badge-outline
        </v-icon>
      </v-btn>
      <v-btn text style="color: white; font-family: Kumbh Sans; font-size: small; margin-right: 5%;" elevation="0" @click="logout()">
        <span style="color: #424242; text-transform: capitalize;">
          Log out
        </span>
      </v-btn>
    </v-row>
    <v-row style="display: flex; align-items: center; margin-top: 6.5%; margin-left: 2%; font-family: Kumbh Sans; font-weight: bold;">
      <v-btn disabled style="color: white; height:200%; background-color: rgba(0, 0, 0, 0) !important;" elevation="0">
        <span style="color: #C4C4C4; text-transform: capitalize;">
          Add filter
        </span>
        <v-icon color="#C4C4C4">
          mdi-chevron-down
        </v-icon>
      </v-btn>
      <v-icon>mdi-magnify</v-icon>
      <v-text-field
        v-model="search"
        placeholder="Search for a student by name or email"
        solo
        flat
        hide-details
        clearable
        clear-icon="mdi-close-circle-outline"
      />
    </v-row>
    <v-card v-if="isExactMatch" class="mx-auto" style="display: flex; justify-content: center; width: fit-content;">
      <v-card-title>Hola Mundo</v-card-title>
    </v-card>
  </div>
</template>

<script>
export default {
  layout: 'principal',
  data () {
    return {
      search: null,
      teachers: [] // Inicializamos teachers como un array vacío
    }
  },
  mounted () {
    this.token = localStorage.getItem('token')
    this.nombreSchool = localStorage.getItem('nombreSchool')
    this.getAllTeachers()
    this.isExactMatch()
  },
  methods: {
    logout () {
      localStorage.removeItem('token')
      localStorage.removeItem('nombreSchool')
      this.$router.push({ path: '/' })
    },
    getAllTeachers () {
      const url = 'http://localhost:8010/api/auth/get-allteachers/'
      const config = {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      }
      this.$axios.get(url, config)
        .then((res) => {
          if (res.data.message === 'Success') {
          // Filtrar los teachers por nombreSchool
            this.teachers = res.data.teachers.teachers.filter(teacher => teacher.designation === this.nombreSchool)
          } else if (res.data.message === 'Invalid Token') {
            this.$router.push('/')
          }
        })
        .catch((err) => {
          // eslint-disable-next-line no-console
          console.log('@@@ err => ', err)
          if (err.response && err.response.status === 401) {
            this.$router.push('/')
          }
        })
    },
    customFilter (value, search, item) {
      if (!search) { return true }
      return item.fullName.toLowerCase().includes(search.toLowerCase())
    },
    isExactMatch () {
      return this.teachers.some(teacher => teacher.fullName.toLowerCase() === this.search.toLowerCase())
    }
  }
}
</script>
