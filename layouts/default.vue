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
            <img
              src="../static/Statisda.png"
              max-height="26"
              width="96px"
              contain
              class="logo"
            >
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
                  <v-icon color="#fff">
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
