<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      absolute
      temporary
    >
      <v-list-item>
        <v-list-item-icon>
           <v-icon>mdi-database</v-icon>
        </v-list-item-icon>

        <v-list-item-content>
          <v-list-item-title><strong>ProxyDB</strong></v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar dense
      fixed
      app
    >
      <v-app-bar-nav-icon class="hidden-sm-and-up" @click="drawer = true" />
      <v-btn href="/" depressed><v-icon>mdi-database</v-icon>proxydb</v-btn>
          <v-tabs class="ml-5">
          <v-tab class="hidden-xs-only" v-for="(item, i) in items" :key="i" :to="item.to"><v-icon>{{item.icon}}</v-icon>&nbsp;{{item.title}}</v-tab>

        </v-tabs>
    </v-app-bar>

    <v-main>
      <v-container fluid>
        <nuxt />
      </v-container>
    </v-main>
    <!-- <v-footer class="mt-10"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }} - freeproxy.io</span>
    </v-footer> -->
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      drawer: false,
      items: [
        {
          icon: 'mdi-format-list-bulleted',
          title: 'Proxy list',
          to: '/'
        },
        {
          icon: 'mdi-security',
          title: 'Anonymity checker',
          to: '/anon-check'
        },
        {
          icon: 'mdi-chart-bar',
          title: 'DB stats',
          to: '/db'
        },
        {
          icon: 'mdi-heart',
          title: 'Donate',
          to: '/donate'
        },
      ],
      miniVariant: false,
      title: 'Free proxy'
    }
  }
}
</script>
