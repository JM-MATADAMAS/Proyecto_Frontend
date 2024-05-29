<template>
  <v-app dark>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
      elevation="0"
      color="#100F57"
      absolute
      height="150px"
    >
      <v-container fluid>
        <v-row align="center" justify="space-between" no-gutters>
          <v-col cols="auto">
            <v-img
              src="https://s3-alpha-sig.figma.com/img/9a98/bc56/75248163a8e07abbbbb0492141c9529f?Expires=1716768000&Key-Pair-Id=APKAQ4GOSFWCVNEHN3O4&Signature=HSUAYoZkh-ibu8r35PUKWN6su2n7-qckZNOFxk5KJdFT7dIlHQdyiUjMzHPXSwEj9b8RJbK6bKDesjazuWCOoe9Vlplo4-WVSiApi502pR9Rrn3Emv3wQ~HOWTzh4UsDHtKwLrBl5UPIkmDH9G68ZskXWLSoc52d-4VU5Ht4eIH8q1U5ks8MT~hKwWuQAPuB9g6sgATUuVL3PBA3CpGFx5OyM4VN5LhVRsVUwRiTKMT8iY94aHjir1wPn1qF8yC7uEUkK3vGg8LDKX-PHVFAkX70SRONw~wM3QoQ5tRfrbjBSd1UG1QuQnk3oqXPUoTu9eDl9opLEUfqCpJ~S~jMhA__"
              max-height="26"
              max-width="98px"
              contain
              class="logo"
            />
          </v-col>
          <v-spacer />
          <v-col class="d-none d-md-flex" cols="auto">
            <v-row align="center" justify="center" no-gutters>
              <v-btn
                v-for="(item, i) in items"
                :key="i"
                :to="item.to"
                router
                exact
                text
                plain
                color="white"
                class="fuente text-capitalize mx-2"
              >
                {{ item.title }}
              </v-btn>
            </v-row>
          </v-col>
          <v-spacer />
          <v-col class="d-none d-md-flex" cols="auto">
            <v-btn
              rounded
              large
              elevation="0"
              color="#0A92DD"
              class="fuente login-btn"
              @click="Login()"
            >
              <span style="color: white; text-transform: capitalize;">
                Login
              </span>
            </v-btn>
          </v-col>
          <v-spacer />
          <v-col cols="auto" class="d-md-none">
            <v-menu offset-y>
              <template #activator="{ on, attrs }">
                <v-btn icon v-bind="attrs" v-on="on">
                  <v-icon color="white">
                    mdi-menu
                  </v-icon>
                </v-btn>
              </template>
              <v-list>
                <v-list-item
                  v-for="(item, i) in items"
                  :key="i"
                  :to="item.to"
                  router
                >
                  <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item>
                <v-list-item>
                  <v-btn
                    text
                    large
                    elevation="0"
                    class="fuente"
                    style="color:#0A92DD; width: 100%;"
                    @click="Login()"
                  >
                    Login
                  </v-btn>
                </v-list-item>
              </v-list>
            </v-menu>
          </v-col>
        </v-row>
      </v-container>
    </v-app-bar>
    <v-main>
      <Nuxt />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        { title: 'Home', to: '/' },
        { title: 'Pricing'/*, to: '/Pricing' */ },
        { title: 'Use Cases'/*, to: '/UseCases' */ },
        { title: 'Location'/*, to: '/Location' */ },
        { title: 'FAQ'/*, to: '/FAQ' */ },
        { title: 'Company'/*, to: '/Company' */ }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  },
  methods: {
    Login () {
      this.$router.push({
        path: '/login/'
      })
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Karla:ital,wght@0,200..800;1,200..800&display=swap');

.login-btn {
  white-space: nowrap;
}

.fuente {
  font-family: "Karla", sans-serif;
  font-optical-sizing: auto;
  font-weight: regular;
  font-style: normal;
}

.logo {
  margin-left: 151px;
}

@media (max-width: 1050px) {
  .logo {
    margin-left: 50px; /* Ajusta según sea necesario */
  }
}

@media (max-width: 960px) {
  .logo {
    margin-left: 0;
    max-width: 50px; /* Ajusta el tamaño según sea necesario */
  }
}
</style>
