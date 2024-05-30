<template>
  <div>
    <v-row style="font-weight: bold; margin-top: 1%; margin-left: 5%; margin-bottom:4% ;font-family: Kumbh Sans;">
      <v-spacer />
      <v-btn icon>
        <v-icon>
          mdi-bell-badge-outline
        </v-icon>
      </v-btn>
      <v-btn text style="color: white; font-family: Kumbh Sans; font-size: small; margin-right: 5%;" elevation="0" @click="logout()">
        <span style="color: #424242; text-transform: capitalize;">
          Log out
        </span>
      </v-btn>
    </v-row>
    <v-row />
    <v-card elevation="0">
      <v-col cols="10">
        <v-row style="margin-top: 9%; margin-left: 10%; font-family: Kumbh Sans; font-size: xx-large; color: #4F4F4F;">
          Add Teachers
          <v-spacer />
          <v-text-field
            v-model="designationTeacher"
            label="Designation"
            outlined
            dense
          />
        </v-row>
        <v-row style="margin-left: 8%; font-family: Kumbh Sans; color: #4F4F4F;">
          <v-btn text style="color: white;">
            <span style="color: #424242; text-transform: capitalize; font-size: 18px;">
              Manualy
            </span>
          </v-btn>
          <v-btn text style="color: white; margin-left: 3%">
            <span style="color: #424242; text-transform: capitalize; font-size: 18px;">
              Import CSV
            </span>
          </v-btn>
        </v-row>
      </v-col>
      <v-col cols="8" style="margin-left: 8%; margin-top: 3%; font-family: Kumbh Sans; color: #4F4F4F;">
        <v-text-field
          v-model="nameTeacher"
          label="Full name"
          outlined
          dense
        />
      </v-col>
    </v-card>
  </div>
</template>

<script>
export default {
  layout: 'principal',
  data: () => {
    return ({
      designationTeacher: null,
      nameTeacher: null
    })
  },
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
