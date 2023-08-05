<template>
  <v-app>
    <v-row>
      <v-navigation-drawer>
        <v-list>
          <v-list-item>Kelas 1</v-list-item>
          <v-list-item>Kelas 2</v-list-item>
          <v-list-item>Kelas 3</v-list-item>
          <v-list-item>Kelas 4</v-list-item>
          <v-list-item>Kelas 5</v-list-item>
          <v-list-item>Kelas 6</v-list-item>
        </v-list>
      </v-navigation-drawer>
      <v-main>
        <v-container>
          <Nuxt />
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
    }
  },
}
</script>
