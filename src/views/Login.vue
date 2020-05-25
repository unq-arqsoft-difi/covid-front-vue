<template>
  <v-content>
    <v-container>
      <v-img
        :src="require('../assets/logo.png')"
        alt="DiFi Ecosystem"
        contain
        class="shrink mr-2"
        height="100"
      />
      <v-card width="400" class="mx-auto mt-5">
        <v-card-title>
          <h1 class="display-1">Login</h1>
        </v-card-title>
        <v-card-text>
          <v-form ref="form">
            <v-text-field label="Username" prepend-icon="mdi-account" required></v-text-field>
            <v-text-field label="Password" prepend-icon="mdi-lock" type="password" required></v-text-field>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-btn color="success" @click="login">Ingresar</v-btn>
          <v-spacer></v-spacer>
          <v-btn text @click="registry">Registrarse</v-btn>
        </v-card-actions>
      </v-card>
    </v-container>
  </v-content>
</template>


<script>
export default {
  name: "Login",
  methods: {
    registry: function() {
      this.$router.push({ name: 'Register' });
    }
  }
};
</script>
