<template>
  <v-app>
    <v-app-bar app color="orange darken-4" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://www.splash-toys.com/assets/themes/krea-theme/img/perso-jo.png"
          transition="scale-transition"
          width="60"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://www.splash-toys.com/assets/themes/krea-theme/img/splash-toys.svg"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn v-if="currentUser" text>
        <span class="mr-2" @click.prevent="logout">Cerrar Sesión</span>
      </v-btn>
    </v-app-bar>
    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
import firebase from "firebase";
import { mapState, mapActions } from "vuex";
export default {
  name: "App",

  data: () => ({}),
  computed: {
    ...mapState(["currentUser"]),
  },
  methods: {
    ...mapActions(["setCurrentUser"]),
    logout() {
      firebase
        .auth()
        .signOut()
        .then(() => {
          this.setCurrentUser(null);
          this.$router.push("/login");
        });
    },
  },
  created() {
    this.setCurrentUser(firebase.auth().currentUser);
  },
};
</script>
