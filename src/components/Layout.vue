<template>
    <v-app dark>
      <v-navigation-drawer app v-model="drawer" :permanent="drawer" hide-overlay width="200" v-if="$auth.user()">
        <v-toolbar flat class="transparent">
          <v-list class="pa-0">
            <v-list-tile avatar>
              <v-list-tile-avatar>
                <img :src="$auth.user().photoURL" >
              </v-list-tile-avatar>
              <v-list-tile-content>
                <v-list-tile-title>{{ $auth.user().displayName || $auth.user().email }}</v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
          </v-list>
        </v-toolbar>
        <v-list>
          <v-list-tile @click="$router.push('/app')">
            <v-list-tile-content>
              <v-list-tile-title>Realtime database</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile @click="$router.push('/firestore')">
            <v-list-tile-content>
              <v-list-tile-title>Cloud firestore</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile>
            <v-list-tile-content @click="$router.push('/profile')">
              <v-list-tile-title>Update profile</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
          <v-list-tile @click="logout()">
            <v-list-tile-content>
              <v-list-tile-title>Logout</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
      </v-navigation-drawer>
      <v-toolbar app >
        <v-toolbar-side-icon @click.native="drawer = !drawer" v-if="$auth.user()"></v-toolbar-side-icon>
        <v-toolbar-title>Myfirebase</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-toolbar-items class="hidden-sm-and-down">
          <v-btn flat>Docs</v-btn>
          <v-btn flat>Github</v-btn>
          <v-btn flat v-if="$auth.user()" @click="logout()">SignOut</v-btn>
        </v-toolbar-items>
      </v-toolbar>
      <v-content>
        <v-container>
          <router-view></router-view>
        </v-container>
      </v-content>
      <v-footer app></v-footer>
    </v-app>
</template>
<script>
import navbar from "./../components/partials/Navbar";
export default {
  mounted () {
    this.$auth
      .check()
      .then(user => {})
      .catch(err => {})
  },
  data () {
    return {
      message: "Welcome Myfirebase SPA framework",
      items: [
        { title: 'Real time Database', link: 'dashboard' },
        { title: 'Cloud Firestore', link: 'account_box' },
      ],
      drawer: true
    }
  },
  methods: {
    logout () {
      this.$auth.logout()
    }
  },
  components: {
    navbar
  }
}
</script>

<style>
.flex {
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>