<script setup lang="ts">
  import { ref } from 'vue';
  import axios from 'axios';

  const email = ref('');
  const password = ref('');

  function login (){
    axios.defaults.withCredentials = true;
    axios.defaults.withXSRFToken = true;
    axios.get('http://localhost:8000/sanctum/csrf-cookie')
      .then(() => {
        axios.post('http://localhost:8000/api/login', {
          email: 'test@example.com',
          password: 'password',
        })
      })
  }

</script>

<template>
  <v-row class="d-flex mb-3">
    <v-col cols="12">ont-weight-bold mb-1">E-mail</v-label>
      <v-text-field v-model="email" color="primary" hide-details variant="outlined" />
    </v-col>
    <v-col cols="12">
      <v-label class="font-weight-bold mb-1">Senha</v-label>
      <v-text-field
        v-model="password"
        color="primary"
        hide-details
        type="password"
        variant="outlined"
      />
    </v-col>
    <v-col class="pt-0" cols="12">
      <div class="d-flex flex-wrap align-center">
        <div class="ml-sm-auto">
          <RouterLink
            class="text-primary text-decoration-none text-body-1 opacity-1 font-weight-medium"
            to="/"
          >Esqueceu sua senha?</RouterLink>
        </div>
      </div>
    </v-col>
    <v-col class="pt-0" cols="12">
      <v-btn
        block
        color="primary"
        flat
        size="large"
        @click="login()"
      >Entrar</v-btn>
    </v-col>
  </v-row>
  <div>
    <h6 class="text-h6 text-muted font-weight-medium d-flex justify-center align-center mt-3">
      Novo no AgendaMe?
      <RouterLink
        class="text-primary text-decoration-none text-body-1 opacity-1 font-weight-medium pl-2"
        :to="{ name: 'register' }"
      >
        Crie sua conta</RouterLink>
    </h6>
  </div>
</template>
