<!-- eslint-disable vue/no-v-text-v-html-on-component -->
<template>
  <v-app dark>
    <v-navigation-drawer permanent color="#152259" style="height: 100%; max-width: 50%;">
      <v-list>
        <v-list-item>
          <v-avatar size="65" class="mx-auto" style="margin-top: 15px;">
            <img src="../static/logo.png" alt="image">
          </v-avatar>
        </v-list-item>
        <v-list-item dense style="margin-bottom: 30px;">
          <v-list-item-content>
            <v-list-item-title class="text-center" style="color: white; font: Kumbh Sans; font-size: medium; margin-top: 20px;">
              Udemy Inter. school
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-divider color="#BDBDBD" />
      <v-list
        nav
        dense
        dark
        style="margin-left: 7%; margin-right: 7%;"
      >
        <v-list-item-group
          v-model="selectedItem"
          color="primary"
        >
          <v-list-item
            v-for="(item, i) in items"
            :key="i"
            :style="{ backgroundColor: selectedItem === i ? '#509CDB' : 'transparent', opacity: 1 }"
            @click="toggleItem(i)"
          >
            <v-list-item-icon>
              <v-icon color="white" v-text="item.icon" />
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title style="color: white; font-size: small;" v-text="item.text" />
            </v-list-item-content>

            <v-list-item-icon v-if="item.children && item.children.length">
              <v-icon color="white">
                mdi-chevron-down
              </v-icon>
            </v-list-item-icon>
          </v-list-item>
          <v-list-group
            v-for="(child, j) in items[selectedItem]?.children || []"
            :key="j"
            no-action
            sub-group
          >
            <template #activator>
              <v-list-item>
                <v-list-item-content>
                  <v-list-item-title style="color: white; font-size: small;" v-text="child.text" />
                </v-list-item-content>
              </v-list-item>
            </template>
          </v-list-group>
        </v-list-item-group>
        <v-list-item style="margin-top: 71%; margin-bottom: 71%;">
          <v-list-item-icon>
            <v-icon color="white">
              mdi-bank-outline
            </v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title style="color: white; font-size: small;">
              Features
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    selectedItem: 0,
    items: [
      { text: 'Dashboard', icon: 'mdi-home-outline' },
      {
        text: 'Teachers',
        icon: 'mdi-home-outline',
        children: [
          { text: 'Teacher 1' },
          { text: 'Teacher 2' }
        ]
      },
      {
        text: 'Students/ classes',
        icon: 'mdi-school-outline',
        children: [
          { text: 'Class 1' },
          { text: 'Class 2' }
        ]
      },
      {
        text: 'Billing',
        icon: 'mdi-bank-outline',
        children: [
          { text: 'Invoice 1' },
          { text: 'Invoice 2' }
        ]
      },
      { text: 'Settings and profile', icon: 'mdi-cog-outline' },
      { text: 'Exams', icon: 'mdi-chart-box-outline' }
    ]
  }),
  methods: {
    toggleItem (index) {
      this.selectedItem = this.selectedItem === index ? null : index
    }
  }
}
</script>
