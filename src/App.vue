<template>
  <v-app>
    <v-card>
      <v-app-bar app color="cyan darken-1" lights-out dark>
        <div class="d-flex align-center">
          <v-img
            alt="Vuetify Logo"
            class="shrink mr-2"
            contain
            src="https://image.flaticon.com/icons/png/512/281/281482.png"
            transition="scale-transition"
            width="40"
          />

          <v-img
            alt="Vuetify Name"
            class="shrink mt-1 hidden-sm-and-down"
            contain
            min-width="100"
            src="https://mijugueteria.com.ec/wp-content/uploads/2016/09/logo-mj.png"
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
    </v-card>
  </v-app>
</template>

<script>
import firebase from "firebase";
import { mapState, mapActions } from "vuex";
export default {
  name: "App",
  data: () => ({
    //
  }),
    computed: {
    ...mapState(["currentUser"]),
  },
  methods: {
    ...mapActions(["updateCurrentUser"]),
    logout() {
      firebase
        .auth()
        .signOut()
        .then(() => {
          this.updateCurrentUser(null);
          this.$router.push("/login");
        });
        },
    },

  created() {
    this.updateCurrentUser(firebase.auth().currentUser);
  },
};
</script>
