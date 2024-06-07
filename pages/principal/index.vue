<template>
  <div>
    <v-row class="text-bold my-1 mx-5 font-kumbh-sans">
      Learn how to launch faster
      <v-spacer v-for="i in 9" :key="i" />
      <v-btn icon>
        <v-icon>
          mdi-bell-outline
        </v-icon>
      </v-btn>
      <v-btn
        color="#509CDB"
        class="font-kumbh-sans small-text"
        style="color: #fff;"
        elevation="0"
        @click="logout"
      >
        <span class="text-capitalize" style="color: #fff;">Log out</span>
      </v-btn>
    </v-row>
    <v-row class="font-kumbh-sans mx-5 my-5">
      watch our webinar for tips from our experts and get a limited time offer.
    </v-row>
    <h1 class="text-color-secondary mt-7 mx-5 font-kumbh-sans">
      Welcome to your dashboard, Udemy school
    </h1>
    <h2 class="text-color-secondary my-10 mx-11 font-kumbh-sans">
      Uyo/school/@teachable.com
    </h2>
    <v-row class="mt-6 mx-8-2 my-5 font-kumbh-sans text-large">
      <img src="../../static/Frame_30083.png" class="mr-2" style="height: 40px;">
      Add other admins
    </v-row>
    <v-row class="mx-13-5 font-kumbh-sans text-regular small-text">
      Create rich course content and coaching products for your students.
    </v-row>
    <v-row class="mx-13-5 font-kumbh-sans text-regular small-text">
      When you give them a pricing plan, they’ll appear on your site!
    </v-row>
    <v-row class="mt-4 mx-8-2 my-5 font-kumbh-sans text-large">
      <img src="../../static/Frame_30084.png" class="mr-2" style="height: 40px;">
      Add classes
    </v-row>
    <v-row class="mx-13-5 font-kumbh-sans text-regular small-text">
      Create rich course content and coaching products for your students.
    </v-row>
    <v-row class="mx-13-5 font-kumbh-sans text-regular small-text">
      When you give them a pricing plan, they’ll appear on your site!
    </v-row>
    <v-row class="mt-4 mx-8-2 my-5 font-kumbh-sans text-large align-center">
      <img src="../../static/Frame_30085.png" class="mr-2" style="height: 40px;">
      Add students
      <v-spacer v-for="i in 9" :key="i" />
      <v-menu top :close-on-click="closeOnClick">
        <template #activator="{ on, attrs }">
          <v-btn
            color="#152259"
            rounded
            x-large
            width="20%"
            v-bind="attrs"
            class="text-white font-kumbh-sans small-text"
            elevation="0"
            v-on="on"
          >
            <v-icon small class="mr-3-5" style="color: white;">
              mdi-headset
            </v-icon>
            <span class="text-capitalize mr-7" style="color: white;">
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
    </v-row>
    <v-row class="mx-13-5 font-kumbh-sans text-regular small-text">
      Create rich course content and coaching products for your students.
    </v-row>
    <v-row class="mx-13-5 font-kumbh-sans text-regular small-text">
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
      this.$router.push({ path: '/' })
    }
  }
}
</script>

<style>
.text-bold {
  font-weight: bold;
}
.text-color-secondary {
  color: #4F4F4F;
}
.font-kumbh-sans {
  font-family: 'Kumbh Sans', sans-serif;
}
.my-1 {
  margin-top: 1%;
  margin-bottom: 1%;
}
.mx-5 {
  margin-left: 5%;
  margin-right: 5%;
}
.mx-11 {
  margin-left: 11%;
}
.mx-8-2 {
  margin-left: 8.2%;
}
.mx-13-5 {
  margin-left: 13.5%;
}
.mt-7 {
  margin-top: 7%;
}
.mt-2 {
  margin-top: 2%;
}
.mt-6 {
  margin-top: 6%;
}
.mt-4 {
  margin-top: 4%;
}
.text-large {
  font-size: x-large;
  font-weight: 500;
}
.text-regular {
  font-weight: 400;
}
.small-text {
  font-size: 14px;
}
.mr-2 {
  margin-right: 2%;
}
.mr-3-5 {
  margin-right: 3.5%;
}
.mr-7 {
  margin-right: 7%;
}
.text-capitalize {
  text-transform: capitalize;
}
.align-center {
  align-items: center;
}
</style>
