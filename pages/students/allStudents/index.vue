<template>
  <div>
    <!-- Barra superior -->
    <v-row style="margin-top: 1%; margin-left: 5%;">
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
    <v-row style="margin-top: 02%; margin-left: 2%; font-family: Kumbh Sans;">
      Students
      <v-spacer />
      <v-btn text style="color: white; font-family: Kumbh Sans; font-size: small; margin-right: 0.7%;" elevation="0">
        <span style="color: #2671B1; text-transform: capitalize;">
          Import CSV
        </span>
      </v-btn>
      <v-btn color="#509CDB" style="color: white; font-family: Kumbh Sans; font-size: small; margin-right: 5%;" elevation="0" @click="$router.push({ path: '/students/addStudents'})">
        <span style="color: #ffffff; text-transform: capitalize;">
          Add students
        </span>
      </v-btn>
    </v-row>
    <!-- Si no hay estudiantes -->
    <v-card v-if="students.length < 1">
      <!-- Filtro y búsqueda -->
      <v-row align="center">
        <v-btn disabled style="color: white;" elevation="0">
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
      <!-- Contenido cuando no hay estudiantes -->
      <v-card-text style="text-align: center;">
        <img src="../../../static/no_notification.png" width="340px" style="margin-top: 25%;">
        <div style="font-family: Kumbh Sans; font-weight: 600; font-size: xx-large;">
          No students at this time
        </div>
        <div style="font-family: Kumbh Sans; font-weight: 500;">
          Students will appear here after they enroll in your school.
        </div>
      </v-card-text>
    </v-card>
    <v-col />
    <v-card v-if="students.length > 0" elevation="0">
      <v-row style="display: flex; align-items: center; margin-top: 3.5%; margin-left: 2%; font-family: Kumbh Sans; font-weight: bold;">
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
      <!-- Tabla de estudiantes -->
      <v-col cols="12">
        <v-row style="display: flex; flex-wrap: nowrap;">
          <v-data-table
            :headers="headers"
            :items="students"
            :search="search"
            :sort-by="['id']"
            :sort-desc="[false]"
            :custom-filter="customFilter"
            style="font-family: Kumbh Sans;"
            @click:row="selectStudent"
          >
            <template #[`item.fullName`]="{ item, index }">
              <v-avatar size="30" left>
                <img v-if="item.genero === 'Male'" :key="`male-${index}`" :src="`https://randomuser.me/api/portraits/men/${index + 1}.jpg`" alt="Avatar">
                <img v-if="item.genero === 'Female'" :key="`female-${index}`" :src="`https://randomuser.me/api/portraits/women/${index + 1}.jpg`" alt="Avatar">
                <img v-if="item.genero == 'Other'" :key="`other-${index}`" :src="`https://randomuser.me/api/portraits/lego/${index +1}.jpg`" alt="Avatar">
              </v-avatar>
              <span>{{ item.fullName }}</span>
            </template>
          </v-data-table>
          <v-card v-if="selectedStudent" elevation="0" style="width: 20%; display: grid; justify-items: center; font-family: Kumbh Sans;">
            <v-card-title style="display: flex; justify-content: center;">
              {{ selectedStudent.id }}
            </v-card-title>
            <v-avatar
              size="80"
              class="mx-auto"
            >
              <img
                v-if="selectedStudentIndex.item.genero == 'Male'"
                :src="`https://randomuser.me/api/portraits/men/${selectedStudentIndex.index + 1}.jpg`"
              >
              <img
                v-if="selectedStudentIndex.item.genero == 'Female'"
                :src="`https://randomuser.me/api/portraits/women/${selectedStudentIndex.index +1 }.jpg`"
              >
              <img
                v-if="selectedStudentIndex.item.genero == 'Other'"
                :src="`https://randomuser.me/api/portraits/lego/${selectedStudentIndex.index +1 }.jpg`"
              >
            </v-avatar>
            <v-row style="margin-top: 5%; padding-bottom: 0%;">
              <v-col style="font-weight: bold;">
                {{ selectedStudent.fullName }}
              </v-col>
            </v-row>
            <v-row style="display: flex; justify-content:center; padding-bottom:8% ;">
              <v-spacer />
              <v-spacer />
              <v-spacer />
              <v-spacer />
              <img src="../../../static/Frame_30086.png" width="30%" height="60%">
              <v-spacer />
              <img src="../../../static/Frame_30087.png" width="30%" height="60%">
              <v-spacer />
              <img src="../../../static/Frame_30088.png" width="30%" height="60%">
              <v-spacer />
              <v-spacer />
              <v-spacer />
              <v-spacer />
            </v-row>
            About
            <v-textarea
              readonly
              outlined
              auto-grow
              value="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam hendrerit consectetur arcu, non vestibulum lacus viverra ut."
              style="font-size: 10px; color: black; padding-bottom: 0%;"
            />
            <v-row style="padding-top: 0%;">
              <v-col>Age:</v-col>
              <v-col>Gender:</v-col>
            </v-row>
            <v-row style="padding-top: 0%;">
              <v-col style="padding-top: 0%;">
                17
              </v-col>
              <v-col style="padding-top: 0%;">
                {{ selectedStudent.genero }}
              </v-col>
            </v-row>
          </v-card>
        </v-row>
      </v-col>
    </v-card>
  </div>
</template>

<script>
export default {
  layout: 'principal',
  data () {
    return {
      search: '',
      headers: [
        { text: 'Name', align: 'start', sortable: false, value: 'fullName' },
        { text: 'StudentID', align: 'start', sortable: false, value: 'id' },
        { text: 'Email address', align: 'start', sortable: false, value: 'email' },
        { text: 'Class', align: 'start', sortable: false, value: 'clase' },
        { text: 'Gender', align: 'start', sortable: false, value: 'genero' }
      ],
      students: [],
      selectedStudent: null,
      selectedStudentIndex: null
    }
  },
  mounted () {
    this.token = localStorage.getItem('token')
    this.nombreSchool = localStorage.getItem('nombreSchool')
    this.getAllStudents()
  },
  methods: {
    logout () {
      localStorage.removeItem('token')
      localStorage.removeItem('nombreSchool')
      this.$router.push({ path: '/' })
    },
    getAllStudents () {
      const url = 'http://localhost:8010/api/auth/get-allstudents/'
      const config = {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      }
      this.$axios.get(url, config)
        .then((res) => {
          if (res.data.message === 'Success') {
          // Filtrar los students por nombreSchool
            this.students = res.data.students.students.filter(student => student.designation === this.nombreSchool)
            // eslint-disable-next-line no-console
            console.log(this.students)
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
      return item.fullName.toLowerCase().includes(search.toLowerCase()) || item.email.toLowerCase().includes(search.toLowerCase())
    },
    selectStudent (student, index) {
      this.selectedStudent = student
      this.selectedStudentIndex = index
    }
  }
}
</script>
