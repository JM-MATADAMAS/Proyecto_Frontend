<template>
  <div>
    <v-row style="margin-top: 1%; margin-left: 5%;">
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
    <v-row style="font-weight: bold; margin-top: 3%; margin-left: 2%; font-family: Kumbh Sans;">
      Teachers
      <v-spacer />
      <v-btn text style="color: white; font-family: Kumbh Sans; font-size: small; margin-right: 0.7%;" elevation="0">
        <span style="color: #2671B1; text-transform: capitalize;">
          Import CSV
        </span>
      </v-btn>
      <v-btn color="#509CDB" style="color: white; font-family: Kumbh Sans; font-size: small; margin-right: 5%;" elevation="0" @click="$router.push({ path: '/teachers/addTeachers'})">
        <span style="color: #ffffff; text-transform: capitalize;">
          Add Teachers
        </span>
      </v-btn>
    </v-row>
    <v-card v-if="teachers.length < 1" elevation="0" class="mx-auto" style="display: flex; flex-direction: column; width:fit-content ; align-content: center; align-items: center;  padding: 0 0 0 0;">
      <v-row style="font-weight: bold; margin-top: 3.5%; margin-left: 2%; font-family: Kumbh Sans; display: flex; align-items: center;">
        <v-btn disabled style="color: white; height:200%; background-color: rgba(0, 0, 0, 0) !important;" elevation="0">
          <span style="color: #C4C4C4; text-transform: capitalize;">
            Add filter
          </span>
          <v-icon color="#C4C4C4">
            mdi-chevron-down
          </v-icon>
        </v-btn>
        <v-text-field
          v-model="search"
          placeholder="Search for a teacher by name"
          solo
          flat
          hide-details
          clearable
          clear-icon="mdi-close-circle-outline"
        />
      </v-row>
      <v-card-text style="margin-top:65% ; font-family: Kumbh Sans; font-weight: 600; font-size: xx-large;">
        No Teachers at this time
      </v-card-text>
      <v-card-text class="mx-auto" style="font-family: Kumbh Sans; font-weight: 500; ">
        Teachers will appear here after they enroll in your school.
      </v-card-text>
    </v-card>
    <v-card v-if="teachers.length > 0" elevation="0">
      <v-row style="display: flex; align-items: center; margin-top: 3.5%; margin-left: 2%; font-family: Kumbh Sans; font-weight: bold;">
        <v-btn disabled style="color: white; height:200%; background-color: rgba(0, 0, 0, 0) !important;" elevation="0">
          <span style="color: #C4C4C4; text-transform: capitalize;">
            Add filter
          </span>
          <v-icon color="#C4C4C4">
            mdi-chevron-down
          </v-icon>
        </v-btn>
        <v-text-field
          v-model="search"
          placeholder="Search for a teacher by name"
          solo
          flat
          hide-details
          clearable
          clear-icon="mdi-close-circle-outline"
        />
      </v-row>
      <v-data-table
        :headers="headers"
        :items="teachers"
        :search="search"
        :custom-filter="customFilter"
        hide-default-footer
        style="margin-top: 2%; font-family: Kumbh Sans; font-weight: bold;"
      >
        <template #[`item.fullName`]="{ item, index }">
          <v-avatar size="30" left>
            <img v-if="item.genero == 'Male'" :key="`male-${index}`" :src="`https://randomuser.me/api/portraits/men/${index + 1}.jpg`" alt="Avatar">
            <img v-if="item.genero == 'Female'" :key="`female-${index}`" :src="`https://randomuser.me/api/portraits/women/${index + 1}.jpg`" alt="Avatar">
          </v-avatar>
          <span>{{ item.fullName }}</span>
        </template>
      </v-data-table>
    </v-card>
  </div>
</template>

<script>
export default {
  layout: 'principal',
  data: () => ({
    search: '',
    headers: [
      { text: 'Name', align: 'start', sortable: false, value: 'fullName' },
      { text: 'Subject', align: 'start', sortable: false, value: 'subject' },
      { text: 'Class', align: 'start', sortable: false, value: 'clase' },
      { text: 'Email address', align: 'start', sortable: false, value: 'email' },
      { text: 'Gender', align: 'start', sortable: false, value: 'genero' }
    ],
    teachers: []
  }),
  mounted () {
    this.token = localStorage.getItem('token')
    this.getAllTeachers()
  },
  methods: {
    logout () {
      localStorage.removeItem('token')
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
            this.teachers = res.data.teachers.teachers
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
    }
  }
}
</script>
