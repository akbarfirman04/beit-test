<template>
  <v-app>
    <v-row>
      <v-navigation-drawer class="deep-purple accent-4" dark permanent>
        <v-list class="pa-4">
          <v-list-item class="px-3" link @click="changeTable(0)">
            <v-list-item-content>
              <v-list-item-title>All Items</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-list-item class="px-3" link @click="changeTable(1)">
            <v-list-item-content>
              <v-list-item-title>Kelas 1</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-list-item class="px-3" link @click="changeTable(2)">
            <v-list-item-content>
              <v-list-item-title>Kelas 2</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-list-item class="px-3" link @click="changeTable(3)">
            <v-list-item-content>
              <v-list-item-title>Kelas 3</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-list-item class="px-3" link @click="changeTable(4)">
            <v-list-item-content>
              <v-list-item-title>Kelas 4</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-list-item class="px-3" link @click="changeTable(5)">
            <v-list-item-content>
              <v-list-item-title>Kelas 5</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
          <v-list-item class="px-3" link @click="changeTable(6)">
            <v-list-item-content>
              <v-list-item-title>Kelas 6</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-navigation-drawer>
      <v-main>
        <v-container class="pa-6">
          <Nuxt :show="show" />
        </v-container>
      </v-main>
    </v-row>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js',
      show: 0,
    }
  },
  methods: {
    changeTable(i) {
      this.$router.push(i === 0 ? '/' : '/' + i)
    },
  },
}
</script>
