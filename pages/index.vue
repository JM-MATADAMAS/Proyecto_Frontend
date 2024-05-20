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
          style="color: white; font-size: xx-large; font-weight: 600; font-family: 'Kumbh Sans', sans-serif; text-align: center;"
        >
          Manage your team
        </v-card-title>
        <v-card-title
          color="white"
          class="text-center"
          style="color: white; font-size: xx-large; font-weight: 600; font-family: 'Kumbh Sans', sans-serif; margin-bottom: 16px; text-align: center;"
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
    <v-img
      src="https://s3-alpha-sig.figma.com/img/413f/8a42/730fafa4c464bba9da308b1c2112a48e?Expires=1716768000&Key-Pair-Id=APKAQ4GOSFWCVNEHN3O4&Signature=d8CYGb1SWO0JhGoege4J8MESUhV9rHIS6pxPYDis1jbJj9AANPq-9SKBm48VSRgQ7xzbE8gWl4h1KYnwAQ5MsGdNjKsuiQriSFs~uQhDdBk4xCTEaKXEMGg21~pkR5tQafAdmtvSnNkhewt7Nr8qpJddjlj4f6BiYpq9ZkUeLSdAbH2JUk0~~E1UDBdjEDKanHrFxs1i0XsVnEuCByhYhZDluey0oIKmnQ93rbY0v9kpkPDlWZYo0BviIJUh8b8PVuMGl8sl9GI4jAsrtSAzfMt9BVFZY1cHctnoUZ6xnRNn8YprTJ7YhkNBHxmMKcJx0mG8zkiMl37wU4QhoWpk9w__"
      style="width: 90%; max-width: 931px; margin: 20px auto;"
      contain
    />
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
