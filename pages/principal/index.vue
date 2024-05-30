<template>
  <div>
    <v-row style="font-weight: bold; margin-top: 1%; margin-left: 5%; font-family: Kumbh Sans;">
      Learn  how to launch faster
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-btn icon>
        <v-icon>
          mdi-bell-badge-outline
        </v-icon>
      </v-btn>
      <v-spacer />
      <v-btn color="#509CDB" style="color: white; font-family: Kumbh Sans; font-size: small;" elevation="0" @click="logout()">
        <span style="color: white; text-transform: capitalize;">
          Log out
        </span>
      </v-btn>
      <v-spacer />
    </v-row>
    <v-row style="font-weight:initial; margin-left: 5%; font-family: Kumbh Sans;">
      watch our webinar for tips from our experts and get a limited time offer.
    </v-row>
    <h1 style="color: #4F4F4F; margin-top: 7%; margin-left: 5%; font-family: Kumbh Sans;">
      Welcome to your dashboard, Udemy school
    </h1>
    <h2 style="color: #4F4F4F; margin-top: 2%; margin-left: 11%; font-family: Kumbh Sans;">
      Uyo/school/@teachable.com
    </h2>
    <v-row style="margin-top: 6%; margin-left: 8.2%; font-size: x-large; font-family: Kumbh Sans; font-weight: 500;">
      <img src="../../static/Frame_30083.png" style="height: 40px; margin-right: 2%;">
      Add other admins
    </v-row>
    <v-row style="margin-left: 13.5%; font-family: Kumbh Sans; font-weight: 400; font-size: 14px;">
      Create rich course content and coaching products for your students.
    </v-row>
    <v-row style="margin-left: 13.5%; font-family: Kumbh Sans; font-weight: 400; font-size: 14px;">
      When you give them a pricing plan, they’ll appear on your site!
    </v-row>
    <v-row style="margin-top: 4%; margin-left: 8.2%; font-size: x-large; font-family: Kumbh Sans; font-weight: 500;">
      <img src="../../static/Frame_30084.png" style="height: 40px; margin-right: 2%;">
      Add classes
    </v-row>
    <v-row style="margin-left: 13.5%; font-family: Kumbh Sans; font-weight: 400; font-size: 14px;">
      Create rich course content and coaching products for your students.
    </v-row>
    <v-row style="margin-left: 13.5%; font-family: Kumbh Sans; font-weight: 400; font-size: 14px;">
      When you give them a pricing plan, they’ll appear on your site!
    </v-row>
    <v-row style="margin-top: 4%; margin-left: 8.2%; font-size: x-large; font-family: Kumbh Sans; font-weight: 500;">
      <img src="../../static/Frame_30085.png" style="height: 40px; margin-right: 2%;">
      Add students
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-spacer />
      <v-menu
        top
        :close-on-click="closeOnClick"
      >
        <template #activator="{ on, attrs }">
          <v-btn
            color="#152259"
            rounded
            x-large
            width="20%"
            v-bind="attrs"
            style="color: white; font-family: Kumbh Sans; font-size: small;"
            elevation="0"
            v-on="on"
          >
            <v-icon small style="margin-right: 15%;">
              mdi-headset
            </v-icon>
            <span style="color: white; text-transform: capitalize; margin-right: 35%;">
              Support
            </span>
            <v-icon color="white">
              mdi-chevron-up
            </v-icon>
          </v-btn>
        </template>
        <v-list>
          <v-list-item
            v-for="(item, index) in items"
            :key="index"
          >
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
      <v-spacer />
    </v-row>
    <v-row style="margin-left: 13.5%; font-family: Kumbh Sans; font-weight: 400; font-size: 14px;">
      Create rich course content and coaching products for your students.
    </v-row>
    <v-row style="margin-left: 13.5%; font-family: Kumbh Sans; font-weight: 400; font-size: 14px;">
      When you give them a pricing plan, they’ll appear on your site!
    </v-row>
  </div>
</template>

<script>
export default {
  layout: 'principal',
  data: () => ({
    items: [
      { title: 'Find answers' },
      { title: 'Contact us' },
      { title: 'Suggest an improvement' },
      { title: 'Support page' }
    ],
    closeOnClick: true
  }),
  methods: {
    logout () {
      localStorage.removeItem('token')
      this.$router.push({
        path: '/'
      })
    }
  }
}
</script>
