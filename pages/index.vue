<template>
  <v-sheet max-height="30%" max-width="100%" color="#100F57">
    <div style="display: flex; flex-direction: column; align-items: center;">
      <v-btn
        rounded
        elevation="0"
        color="rgba(255, 255, 255, 0.05)"
        style="width: 90%; max-width: 400px; margin-top: 5%; margin-bottom: 16px;"
        class="fuente"
      >
        <span style="color: rgba(216, 153, 37, 1); text-transform: capitalize;">
          Get your free consultation now
        </span>
      </v-btn>
      <v-card elevation="0" color="#100F57" style="display: flex; flex-direction: column; align-items: center; margin-bottom: 16px;">
        <v-card-title
          color="white"
          class="text-center"
          style="color: white; font-size: 400%; font-weight: 600; font-family: 'Kumbh Sans', sans-serif; text-align: center;"
        >
          Manage your team
        </v-card-title>
        <v-card-title
          color="white"
          class="text-center"
          style="color: white; font-size: 400%; font-weight: 600; font-family: 'Kumbh Sans', sans-serif; margin-bottom: 20px; text-align: center;"
        >
          easily with task man
        </v-card-title>
        <v-card-text
          color="white"
          class="text-center fuente"
          style="color: white; font-size: medium;"
        >
          Statisdaa is a school management solution that
        </v-card-text>
        <v-card-text
          color="white"
          class="text-center fuente"
          style="color: white; font-size: medium;"
        >
          offers a personalized portal to each type of user,
        </v-card-text>
      </v-card>
      <div style="display: flex; justify-content: center;">
        <v-btn
          rounded
          elevation="0"
          color="#0A92DD"
          x-large
          style="width: 90%; max-width: 400px; margin-bottom: 16px;"
        >
          <span style="color: white; text-transform: capitalize;">
            Get Started
          </span>
        </v-btn>
      </div>
    </div>
    <img
      src="@/static/Project_Kanvan.png"
      style="width: 90%; max-width: 931px; margin: 20px auto;  display: flex; justify-content: center;"
      class="mx-auto"
    >
    <v-card elevation="0" style="display: flex; flex-direction: column; align-items: center; margin-top: 5%;">
      <v-card-title
        class="text-center"
        style=" font-size: 2.5vw; font-weight: 600; font-family: 'Kumbh Sans', sans-serif; text-align: center;"
      >
        Trusted by company like
      </v-card-title>
      <v-card-text class="responsive-icons-container" style="margin-top: 2%;">
        <v-spacer />
        <img :src="require('@/static/Standard_Collection_24.png')" alt="Image" class="responsive-icon">
        <v-spacer />
        <img :src="require('@/static/Standard_Collection_29.png')" alt="Image" class="responsive-icon">
        <v-spacer />
        <img :src="require('@/static/Vector.png')" alt="Image" class="responsive-icon">
        <v-spacer />
        <img :src="require('@/static/Standard_Collection_24.png')" alt="Image" class="responsive-icon">
        <v-spacer />
        <img :src="require('@/static/Standard_Collection_29.png')" alt="Image" class="responsive-icon">
        <v-spacer />
        <img :src="require('@/static/Vector.png')" alt="Image" class="responsive-icon">
        <v-spacer />
      </v-card-text>
    </v-card>
    <div class="responsive-image-container">
      <img src="@/static/Frame_8.png" alt="Image" class="responsive-image">
    </div>
    <div class="responsive-image-container">
      <img src="@/static/Frame_10.png" alt="Image" class="responsive-image">
    </div>
    <v-card elevation="0" style="display:flex; align-items: center; flex-direction: column;">
      <v-card-title class="fuente" style="color: #1777F7; font-size: 40px; margin-top: 2%;">
        Pick up the best plan
      </v-card-title>
      <v-card-text class="fuente" style="max-width: 500px; font-size: 20px; text-align: center; color: #667085;">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Purus odio pellentesque pellentesque a. Amet ut lobortis pellentesque a, luctus maecenas.
      </v-card-text>
    </v-card>
  </v-sheet>
</template>

<script>
export default {
  name: 'IndexPage'
}
</script>

<style scoped>
.text-center {
  text-align: center;
}
.fuente {
  font-family: 'Kumbh Sans', sans-serif;
}
.responsive-icons-container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
.responsive-icon {
  width: 5%;
  height: auto;
  max-width: 36px;
  max-height: 33px;
}
@media (max-width: 400px) {
  .responsive-icon {
    width: 10%;
  }
}
.responsive-image-container {
  display: flex;
  justify-content: center;
}
.responsive-image {
  width: 100%;
  height: auto;
  max-width: 1440px;
}
</style>
