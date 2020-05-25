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
          <v-alert v-if="errors.length > 0" type="error">
            <ul>
              <li v-for="(error, i) in errors" :key="i">{{ error }}</li>
            </ul>
          </v-alert>
          <v-form ref="form">
            <v-text-field
              label="E-Mail"
              prepend-icon="mdi-at"
              v-model="email"
              required
            ></v-text-field>
            <v-text-field
              label="Password"
              prepend-icon="mdi-lock"
              type="password"
              v-model="password"
              required
            ></v-text-field>
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
import axios from "axios";
export default {
  name: "Login",
  data() {
    return {
      errors: [],
      email: null,
      password: null,
    };
  },
  methods: {
    login: function() {
      axios
        .post("http://localhost:9001/login", {
          email: this.email,
          pass: this.password,
        })
        .then(() => this.$router.push({ name: "HomePage" }))
        .catch((error) => {
          if (error.response) {
            this.errors = error.response.data.errors;
          } else {
            this.errors = ["Something is wrong... try again"];
          }
        });
    },
    registry: function() {
      this.$router.push({ name: "Register" });
    },
  },
};
</script>
