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
      <v-card color="#e6e9fd" width="400" class="mx-auto mt-5">
        <v-card-title>
          <h1 class="display-1">Registro</h1>
        </v-card-title>
        <v-card-text>
          <v-alert v-if="errors.length > 0" type="error">
            <ul>
              <li v-for="(error, i) in errors" :key="i">{{ error }}</li>
            </ul>
          </v-alert>
          <v-form ref="form">
            <v-row>
              <v-col cols="6">
                <v-text-field
                  label="Nombre"
                  prepend-icon="mdi-id-card"
                  v-model="registryData.firstName"
                  :rules="[rules.required]"
                  required></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  label="Apellido"
                  prepend-icon="mdi-id-card"
                  v-model="registryData.lastName"
                  :rules="[rules.required]"
                  required></v-text-field>
              </v-col>
            </v-row>

            <v-row>
              <v-col cols="6">
                <v-text-field
                  label="E-Mail"
                  prepend-icon="mdi-at"
                  v-model="registryData.email"
                  :rules="[rules.required]"
                  required></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  label="Teléfono"
                  prepend-icon="mdi-phone"
                  v-model="registryData.phone"
                  :rules="[rules.required]"
                  required></v-text-field>
              </v-col>
            </v-row>

            <v-row>
              <v-col cols="6">
                <v-text-field
                  label="Entidad"
                  prepend-icon="mdi-hospital-building"
                  v-model="registryData.entity"
                  :rules="[rules.required]"
                  required></v-text-field>
              </v-col>
              <v-col cols="6">
                <v-text-field
                  label="Cargo"
                  prepend-icon="mdi-briefcase"
                  v-model="registryData.job"
                  :rules="[rules.required]"
                  required></v-text-field>
              </v-col>
            </v-row>

            <v-text-field
              label="Localidad"
              prepend-icon="mdi-google-maps"
              v-model="registryData.place"
              :rules="[rules.required]"
              required></v-text-field>
            <v-text-field
              label="Password"
              prepend-icon="mdi-lock"
              type="password"
              v-model="registryData.pass"
              :rules="[rules.required]"
              required></v-text-field>
          </v-form>
          <v-btn
            color="success"
            style="margin-bottom: 5px"
            @click="registry"
            block
            >Registrarse</v-btn
          >
          <v-btn text @click="back" block>Volver</v-btn>
        </v-card-text>
      </v-card>
    </v-container>
  </v-content>
</template>

<script>
import axios from "axios";
export default {
  name: "Register",
  data() {
    return {
      errors: [],
      rules: {
        required: (value) => !!value || "Required.",
      },
      registryData: {
        firstName: null,
        lastName: null,
        email: null,
        phone: null,
        entity: null,
        job: null,
        place: null,
        pass: null,
      },
    };
  },
  methods: {
    back: function() {
      this.$router.go(-1);
    },
    registry: function() {
      axios
        .post("http://localhost:9001/users", this.registryData)
        .then(() => this.$router.push({ name: 'Login' }))
        .catch((error) => {
          if (error.response) {
            this.errors = error.response.data.errors;
          } else {
            this.errors = ["Something is wrong... try again"];
          }
        });
    },
  },
};
</script>
