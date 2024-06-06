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
      <v-btn icon @click="getAllTeachers()">
        <v-icon>mdi-magnify</v-icon>
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
    <v-card v-if="cardDetails == true" elevation="0" class="mx-auto" style="display: flex; padding-top: 7%; font-family: Kumbh Sans;">
      <v-col cols="1" />
      <v-col cols="6">
        <v-row style="display: flex; justify-content:center;">
          <v-avatar size="250" left>
            <img v-if="genero == 'Male'" :src="`https://randomuser.me/api/portraits/men/${100 - (id+1)}.jpg`" alt="Avatar">
            <img v-if="genero == 'Female'" :src="`https://randomuser.me/api/portraits/women/${100 - (id+1)}.jpg`" alt="Avatar">
          </v-avatar>
        </v-row>
        <v-row style="display: flex; justify-content:center;">
          <v-card-title style="padding-top: 6%; font-weight: bold;">
            {{ nameTeacher }}
          </v-card-title>
        </v-row>
        <v-row style="display: flex; justify-content:center;">
          <v-card-title style="padding-top: 0%; color: #A7A7A7;">
            {{ subject }} teacher
          </v-card-title>
        </v-row>
        <v-row style="display: flex; justify-content:center;">
          <v-spacer />
          <v-spacer />
          <v-spacer />
          <v-spacer />
          <img src="../../../static/Frame_30086.png" width="61px">
          <v-spacer />
          <img src="../../../static/Frame_30087.png" width="61px">
          <v-spacer />
          <img src="../../../static/Frame_30088.png" width="61px">
          <v-spacer />
          <v-spacer />
          <v-spacer />
          <v-spacer />
        </v-row>
      </v-col>
      <v-col cols="6">
        <v-row style="display: flex; justify-content:flex-start;">
          <v-card-title>About</v-card-title>
        </v-row>
        <v-row style="display: flex; justify-content:flex-start; max-width: 45%; padding-top: 0%;">
          <v-card-text>Nulla Lorem mollit cupidatat irure. Laborum magna nulla duis ullamco cillum dolor. Voluptate exercitation incididunt aliquip deserunt reprehenderit elit laborum. Nulla Lorem mollit cupidatat irure. Laborum magna nulla duis ullamco cillum dolor. Voluptate exercitation incididunt aliquip deserunt reprehenderit elit laborum. </v-card-text>
        </v-row>
        <v-row style="display: flex; justify-content:flex-start;">
          <v-card-title>Age: </v-card-title>
          <v-spacer />
          <v-card-title>Gender: </v-card-title>
          <v-spacer />
          <v-spacer />
          <v-spacer />
        </v-row>
        <v-row style="display: flex; justify-content:flex-start;">
          <v-card-title>34 </v-card-title>
          <v-spacer />
          <v-card-title>{{ genero }} </v-card-title>
          <v-spacer />
          <v-spacer />
          <v-spacer />
        </v-row>
        <v-row style="display: flex; justify-content:flex-start;">
          <avatar-group :avatars="avatarList" />
        </v-row>
      </v-col>
    </v-card>
  </div>
</template>

<script>
import axios from 'axios'
import AvatarGroup from '../../../components/ui-components/AvatarGroup.vue'

export default {
  components: {
    AvatarGroup
  },
  layout: 'principal',
  data () {
    return {
      search: null,
      teachers: [],
      cardDetails: false,
      nameTeacher: null,
      subject: null,
      id: null,
      genero: null,
      avatarList: [
        { src: 'https://randomuser.me/api/portraits/women/1.jpg' },
        { src: 'https://randomuser.me/api/portraits/men/2.jpg' },
        { src: 'https://randomuser.me/api/portraits/women/3.jpg' }
        // Añade más avatares según sea necesario
      ]
    }
  },
  mounted () {
    this.token = localStorage.getItem('token')
    this.nombreSchool = localStorage.getItem('nombreSchool')
  },
  methods: {
    logout () {
      localStorage.removeItem('token')
      localStorage.removeItem('nombreSchool')
      this.$router.push({ path: '/' })
    },
    async getAllTeachers () {
      const url = 'http://localhost:8010/api/auth/get-allteachers/'
      const config = {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      }
      const response = await axios.get(url, config)
      const body = response.data.teachers.teachers.filter(teacher => teacher.designation === this.nombreSchool)
      // eslint-disable-next-line no-console
      console.log(body)
      for (let i = 0; i < body.length; i++) {
        if (this.search === body[i].fullName) {
          this.cardDetails = true
          this.nameTeacher = body[i].fullName
          this.id = i
          this.genero = body[i].genero
          this.subject = body[i].subject
          break
        } else {
          this.cardDetails = false
        }
      }
    },
    customFilter (value, search, item) {
      if (!search) { return true }
      return item.fullName.toLowerCase().includes(search.toLowerCase())
    }
  }
}
</script>
