<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      app
      color="#152259"
      :temporary="$vuetify.breakpoint.smAndDown"
      :permanent="!$vuetify.breakpoint.smAndDown"
      style="height: 100%; max-width: 60%;"
    >
      <!-- Contenido del drawer -->
      <v-list>
        <v-list-item>
          <v-avatar size="65" class="mx-auto" style="margin-top: 15px;">
            <img src="../static/logo.png" alt="image">
          </v-avatar>
        </v-list-item>
        <v-list-item dense style="margin-bottom: 10px;">
          <v-list-item-content>
            <v-list-item-title
              class="text-center"
              style="color: white; font-family: 'Kumbh Sans'; font-size: medium; font-weight: bold; margin-top: 20px;"
            >
              Udemy Inter. school
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-divider color="#BDBDBD" />
      <v-list nav dense style="margin-left: 7%; margin-right: 7%;">
        <v-list-item>
          <v-btn
            block
            color="#152259"
            elevation="0"
            class="mx-auto"
            style="color: #ffffff; font-size: 11px; justify-content: flex-start;"
            @click="$router.push({ path: '/principal/'})"
          >
            <v-icon color="white" style="margin-right: 8%;">
              mdi-home-outline
            </v-icon>
            Dashboard
          </v-btn>
        </v-list-item>
        <v-list-item>
          <v-expansion-panels>
            <v-expansion-panel
              style="background-color: #152259; color: white;"
              elevation="0"
            >
              <v-expansion-panel-header
                class="text-left"
                style="padding-left: 4px; font-size: 14px"
              >
                <v-icon color="white">
                  mdi-home-outline
                </v-icon>
                Teachers
                <v-spacer />
                <template #actions>
                  <v-icon color="white">
                    mdi-chevron-down
                  </v-icon>
                </template>
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <v-btn
                  text
                  block
                  color="white"
                  style="font-size: x-small;"
                  class="mx-auto"
                  @click="$router.push({ path: '/teachers/allTeachers'})"
                >
                  <v-icon color="white">
                    mdi-chevron-right
                  </v-icon>
                  All teachers
                </v-btn>
                <v-btn
                  text
                  block
                  color="white"
                  style="font-size: x-small;"
                  class="mx-auto"
                  @click="$router.push({ path: '/teachers/addTeachers'})"
                >
                  <v-icon color="white">
                    mdi-chevron-right
                  </v-icon>
                  Add teachers
                </v-btn>
                <v-btn
                  text
                  block
                  color="white"
                  style="font-size: x-small;"
                  class="mx-auto"
                  @click="$router.push({ path: '/teachers/teacherDetails'})"
                >
                  <v-icon color="white">
                    mdi-chevron-right
                  </v-icon>
                  Teacher details
                </v-btn>
              </v-expansion-panel-content>
            </v-expansion-panel>
            <v-expansion-panel
              style="background-color: #152259; color: white;"
              elevation="0"
            >
              <v-expansion-panel-header
                class="text-left"
                style="padding-left: 16px; font-size: 14px"
              >
                <v-icon color="white" style="margin-right: 15px;">
                  mdi-school-outline
                </v-icon>
                Students/Classes
                <v-spacer />
                <template #actions>
                  <v-icon color="white">
                    mdi-chevron-down
                  </v-icon>
                </template>
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <v-btn
                  text
                  block
                  color="white"
                  style="font-size: x-small;"
                  class="mx-auto"
                  @click="$router.push({ path: '/students/allStudents'})"
                >
                  <v-icon color="white">
                    mdi-chevron-right
                  </v-icon>
                  All students
                </v-btn>
                <v-btn
                  text
                  block
                  color="white"
                  style="font-size: x-small;"
                  class="mx-auto"
                  @click="$router.push({ path: '/students/admissionForms/'})"
                >
                  <v-icon color="white">
                    mdi-chevron-right
                  </v-icon>
                  Admission Form
                </v-btn>
                <v-btn
                  text
                  block
                  color="white"
                  style="font-size: x-small;"
                  class="mx-auto"
                  @click="$router.push({ path: '/students/studentPromotion/'})"
                >
                  <v-icon color="white">
                    mdi-chevron-right
                  </v-icon>
                  Student Promotion
                </v-btn>
                <v-btn
                  text
                  block
                  color="white"
                  style="font-size: x-small;"
                  class="mx-start"
                  @click="$router.push({ path: '/students/class/'})"
                >
                  <v-icon color="white">
                    mdi-chevron-right
                  </v-icon>
                  Class
                </v-btn>
              </v-expansion-panel-content>
            </v-expansion-panel>
            <v-expansion-panel
              style="background-color: #152259; color: white;"
              elevation="0"
            >
              <v-expansion-panel-header
                class="text-left"
                style="padding-left: 2px; font-size: 14px"
              >
                <v-icon color="white">
                  mdi-bank-outline
                </v-icon>
                Billing
                <v-spacer />
                <template #actions>
                  <v-icon color="white">
                    mdi-chevron-down
                  </v-icon>
                </template>
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <v-btn
                  text
                  block
                  color="white"
                  style="font-size: x-small;"
                  class="mx-auto"
                  @click="$router.push({ path: '/billing/studentBilling/'})"
                >
                  <v-icon color="white">
                    mdi-chevron-right
                  </v-icon>
                  Student Billing
                </v-btn>
                <v-btn
                  text
                  block
                  color="white"
                  style="font-size: x-small;"
                  class="mx-auto"
                  @click="$router.push({ path: '/billing/parentBilling/'})"
                >
                  <v-icon color="white">
                    mdi-chevron-right
                  </v-icon>
                  Parent Billing
                </v-btn>
                <v-btn
                  text
                  block
                  color="white"
                  style="font-size: x-small;"
                  class="mx-auto"
                  @click="$router.push({ path: '/billing/schoolBilling/'})"
                >
                  <v-icon color="white">
                    mdi-chevron-right
                  </v-icon>
                  School Billing
                </v-btn>
                <v-btn
                  text
                  block
                  color="white"
                  style="font-size: x-small;"
                  class="mx-auto"
                  @click="$router.push({ path: '/billing/friendsBilling/'})"
                >
                  <v-icon color="white">
                    mdi-chevron-right
                  </v-icon>
                  Friends Billing
                </v-btn>
              </v-expansion-panel-content>
            </v-expansion-panel>
          </v-expansion-panels>
        </v-list-item>
        <v-list-item>
          <v-btn
            color="#152259"
            elevation="0"
            class="mx-auto"
            style="color: #ffffff; font-size: 10px; justify-content: flex-start;"
          >
            <v-icon color="white" style="margin-right: 5%;">
              mdi-cog-outline
            </v-icon>
            Settings and profile
          </v-btn>
        </v-list-item>
        <v-list-item>
          <v-btn
            block
            color="#152259"
            elevation="0"
            class="mx-auto"
            style="color: #ffffff; font-size: 11px; justify-content: flex-start;"
          >
            <v-icon color="white" style="margin-right: 8%;">
              mdi-chart-box-outline
            </v-icon>
            Exams
          </v-btn>
        </v-list-item>
        <v-list-item>
          <v-btn
            block
            color="#152259"
            elevation="0"
            class="mx-auto"
            style="color: #ffffff; font-size: 11px; justify-content: flex-start;"
          >
            <v-icon color="white" style="margin-right: 8%;">
              mdi-bank-outline
            </v-icon>
            Features
          </v-btn>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-main>
      <v-container>
        <!-- Botón flotante para abrir el drawer -->
        <v-btn
          v-if="$vuetify.breakpoint.smAndDown"
          fab
          elevation="0"
          class="ma-10"
          fixed
          sticky
          top
          right
          @click="drawer = !drawer"
        >
          <v-icon>mdi-menu</v-icon>
        </v-btn>
        <ui-alert
          v-if="showAlert"
          :message="mensaje"
          :color="color"
          :type="type"
        />
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'Principal',
  data () {
    return {
      drawer: true,
      showAlert: false,
      mensaje: '',
      color: '',
      type: ''
    }
  },
  mounted () {
    const token = localStorage.getItem('token')
    if (!token) {
      this.$router.push({
        path: '/login/'
      })
    }
  },
  created () {
    this.$nuxt.$on('evento', (data) => {
      this.mensaje = data.message
      this.color = data.color
      this.type = data.type
      this.showAlert = true
      setTimeout(() => {
        this.showAlert = false
      }, 5000)
    })
  }
}
</script>

<style scoped>

@import url('https://fonts.googleapis.com/css2?family=Kumbh+Sans:wght@400;700&display=swap');

.fuente-kumbh {
  font-family: "Kumbh Sans", sans-serif;
  font-optical-sizing: auto;
  font-weight: weight;
  font-style: normal;
  font-variation-settings:
    "YOPQ" 300;
}

.text-left {
  justify-content: flex-start !important;
}
</style>
