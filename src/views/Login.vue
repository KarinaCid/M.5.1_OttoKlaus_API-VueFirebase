<template>
  <v-app>
      <v-card width="400px" class="mx-auto my-5">
        <v-card-title class="pb-0">
        <h2 class="mx-auto mb-5 pink--text text--darken-1">OTTO KLAUS</h2>
        </v-card-title>
        <v-card-text>
          <v-form>  
            <v-text-field
              label="Correo Electrónico"
              prepend-icon="mdi-account-circle"
              v-model="user"/>
            <v-text-field
              label="Contraseña"
              :type="showPassword ? 'text' : 'password'"
              prepend-icon="mdi-lock"
              :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
              @click:append="showPassword = !showPassword"
              v-model="password"/>
          </v-form>
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="info" @click.prevent="login">Ingresar</v-btn>
        </v-card-actions>
      </v-card>
  </v-app>
</template>

<script>
import { mapActions } from "vuex";
import firebase from "firebase";
export default {
  data() {
    return {
      user: "",
      password: "",
      showPassword: false,
    };
  },
  methods: {
    ...mapActions(["updateCurrentUser"]),
    login() {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.user, this.password)
        .then(() => {
          this.updateCurrentUser(firebase.auth().currentUser);
          this.$router.push("/login ");
        })
        .catch(() => {
          alert("Usuario o Contraseña incorrectos");
        });
    },
  },
  created() {
    this.getApod();
  },
};
</script>