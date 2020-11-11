<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://img.freepik.com/vector-gratis/juguetes-ninos-estanterias-madera_53562-2731.jpg?size=626&ext=jpg"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn v-if="currentUser" @click="logout" text>
        <span class="mr-2">Cerrar Sesión</span>
        <v-icon>mdi-lock-open</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
import firebase from 'firebase'
import {mapState, mapActions} from 'vuex'
export default {
  name: 'App',
  methods: {
    ...mapActions(['updateCurrentUser']),
    logout() {
      firebase.auth().signOut().then(() => {
        this.updateCurrentUser(null)
        this.$router.push('/login')
      })
    }
  },
  computed: {
    ...mapState(['currentUser'])
  },
  created() {
    this.updateCurrentUser(firebase.auth().currentUser)
  }
}
</script>