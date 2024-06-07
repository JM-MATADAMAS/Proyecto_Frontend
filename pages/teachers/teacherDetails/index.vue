<template>
  <v-container fluid>
    <v-row class="mt-1 ml-5">
      <v-btn text class="white--text font-small mr-2.7" elevation="0">
        <span class="blue--text capitalize">
          Export CSV
        </span>
      </v-btn>
      <v-btn class="font-small mr-5" color="#509CDB" elevation="0" @click="$router.push({ path: '/teachers/addTeachers'})">
        <span class="white--text capitalize">
          Add Teachers
        </span>
      </v-btn>
      <v-spacer />
      <v-btn icon>
        <v-badge dot>
          <v-icon>
            mdi-bell-outline
          </v-icon>
        </v-badge>
      </v-btn>
      <v-btn text class="white--text font-small mr-5" elevation="0" @click="logout()">
        <span class="gray--text capitalize">
          Log out
        </span>
      </v-btn>
    </v-row>
    <v-row class="mt-4 ml-2 mb-0 align-center bold-font">
      <v-btn disabled class="white--text h-200 transparent-bg" elevation="0">
        <span class="gray--text capitalize">Add filter</span>
        <v-icon class="gray--text">
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
    <v-card v-if="cardDetails" elevation="0" class="mx-auto d-flex pt-2 font-small" style=" display: flex; align-content: center; flex-wrap: wrap;">
      <v-col cols="12" md="6" style="display: flex; flex-direction: column;">
        <v-row class="justify-center pt-10">
          <v-avatar size="250">
            <img v-if="genero === 'Male'" :src="`https://randomuser.me/api/portraits/men/${100 - (id+1)}.jpg`" alt="Avatar">
            <img v-if="genero === 'Female'" :src="`https://randomuser.me/api/portraits/women/${100 - (id+1)}.jpg`" alt="Avatar">
            <img v-if="genero == 'Other'" :src="`https://randomuser.me/api/portraits/lego/${10-(id+1)}.jpg`" alt="Avatar">
          </v-avatar>
        </v-row>
        <v-row class="justify-center">
          <v-card-title class="pt-6 font-bold">
            {{ nameTeacher }}
          </v-card-title>
        </v-row>
        <v-row class="justify-center">
          <v-card-title class="pt-0 gray--text">
            {{ subject }} teacher
          </v-card-title>
        </v-row>
        <v-row class="justify-center">
          <v-spacer /><v-spacer /><v-spacer /><v-spacer />
          <img src="../../../static/Frame_30086.png" width="61px">
          <v-spacer />
          <img src="../../../static/Frame_30087.png" width="61px">
          <v-spacer />
          <img src="../../../static/Frame_30088.png" width="61px">
          <v-spacer /><v-spacer /><v-spacer /><v-spacer />
        </v-row>
      </v-col>
      <v-col cols="12" md="6" class="pt-0">
        <v-row class="justify-start">
          <v-card-title>About</v-card-title>
        </v-row>
        <v-row class="justify-start max-w-45 pt-0">
          <v-card-text>Nulla Lorem mollit cupidatat irure. Laborum magna nulla duis ullamco cillum dolor. Voluptate exercitation incididunt aliquip deserunt reprehenderit elit laborum. Nulla Lorem mollit cupidatat irure. Laborum magna nulla duis ullamco cillum dolor. Voluptate exercitation incididunt aliquip deserunt reprehenderit elit laborum.</v-card-text>
        </v-row>
        <v-row class="justify-start">
          <v-card-title>Age:</v-card-title>
          <v-spacer />
          <v-card-title>Gender:</v-card-title>
          <v-spacer /><v-spacer /><v-spacer />
        </v-row>
        <v-row class="justify-start">
          <v-card-title>34</v-card-title>
          <v-spacer />
          <v-card-title>{{ genero }}</v-card-title>
          <v-spacer /><v-spacer /><v-spacer />
        </v-row>
        <v-row class="justify-start">
          <v-card-title class="pt-0 pb-1 font-bold">
            Teachers from the same class
          </v-card-title>
        </v-row>
        <v-row class="justify-start" style="padding-top: 2%; padding-bottom: 2%;">
          <avatar-group :avatars="avatarList" />
          <v-card-text class="blue--text underline">
            +12 more
          </v-card-text>
        </v-row>
      </v-col>
    </v-card>
  </v-container>
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
      class: null,
      avatarList: [
        { src: 'https://randomuser.me/api/portraits/women/41.jpg' },
        { src: 'https://randomuser.me/api/portraits/men/42.jpg' },
        { src: 'https://randomuser.me/api/portraits/women/43.jpg' }
      ],
      link: null,
      drawer: false // Añadir esta línea
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
          this.class = body[i].clase
          break
        } else {
          this.cardDetails = false
        }
      }
    }
  }
}
</script>

<style scoped>
.font-small {
  font-size: small;
}
.font-bold {
  font-weight: bold;
}
.gray--text {
  color: #424242;
}
.blue--text {
  color: #2671B1;
}
.underline {
  text-decoration: underline;
}
.h-200 {
  height: 200%;
}
.transparent-bg {
  background-color: rgba(0, 0, 0, 0) !important;
}
</style>
