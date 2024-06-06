<template>
  <v-app dark>
    <v-main style="background-color: #f3f3f3;">
      <ui-alert
        v-if="showAlert"
        :message="mensaje"
        :color="color"
        :type="type"
      />
      <Nuxt />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'LoginLayout',
  data () {
    return {
      showAlert: false,
      mensaje: '',
      color: '',
      type: ''
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
