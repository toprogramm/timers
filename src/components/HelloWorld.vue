<template>
  <v-container>

    <a v-for="(tim, i) in timer" :key="i" :href="tim.href" class="subheading mx-3" >
      {{ tim.text }}
    </a>

  </v-container>

  <v-bottom-navigation>
    <v-btn value="recent">
      <v-icon>mdi-history</v-icon>
      <span>Home</span>
    </v-btn>

    <v-btn value="favorites">
      <v-icon>mdi-heart</v-icon>
      <span>Favorites</span>
    </v-btn>

    <v-btn value="nearby">
      <v-icon>mdi-map-marker</v-icon>
      <span>Back</span>
    </v-btn>
  </v-bottom-navigation>
</template>

<script>

export default {
  name: 'HelloWorld',

  data: () => ({
    timer: [
      {
        text: 'timer',
        href: 'http://localhost:8080/timer',
      },
    ],
    ecosystem: [
      {
        text: 'vuetify-loader',
        href: 'https://github.com/vuetifyjs/vuetify-loader/tree/next',
      },
      {
        text: 'github',
        href: 'https://github.com/vuetifyjs/vuetify/tree/next',
      },
      {
        text: 'awesome-vuetify',
        href: 'https://github.com/vuetifyjs/awesome-vuetify',
      },
    ],
    importantLinks: [
      {
        text: 'Chat',
        href: 'https://community.vuetifyjs.com',
      },
      {
        text: 'Made with Vuetify',
        href: 'https://madewithvuejs.com/vuetify',
      },
      {
        text: 'Twitter',
        href: 'https://twitter.com/vuetifyjs',
      },
      {
        text: 'Articles',
        href: 'https://medium.com/vuetify',
      },
    ],
    whatsNext: [
      {
        text: 'Explore components',
        href: 'https://vuetifyjs.com',
      },
      {
        text: 'Roadmap',
        href: 'https://vuetifyjs.com/introduction/roadmap/',
      },
      {
        text: 'Frequently Asked Questions',
        href: 'https://vuetifyjs.com/getting-started/frequently-asked-questions',
      },
    ],
  }),
}
</script>
