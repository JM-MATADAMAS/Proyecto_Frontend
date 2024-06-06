<template>
  <v-row class="d-flex align-center">
    <v-avatar v-for="(avatar, index) in avatars" :key="index" class="mx-1">
      <v-img :src="avatar.src" />
    </v-avatar>
  </v-row>
</template>

<script>
export default {
  name: 'AvatarGroup',
  props: {
    avatars: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
.v-avatar {
  width: 40px;
  height: 40px;
}
</style>
