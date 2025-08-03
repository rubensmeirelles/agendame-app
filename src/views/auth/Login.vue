<script setup lang="ts">
  import Logo from '@/layouts/full/logo/Logo.vue';
  /* Login form */
  import LoginForm from '@/components/auth/LoginForm.vue';
  import axios from 'axios';

  axios.defaults.withCredentials = true;
  axios.defaults.withXSRFToken = true;
  axios.get('https://agendame-api.test/sanctum/csrf-cookie')
    .then(() => {
      axios.post('https://agendame-api.test/api/login')
    })
</script>
<template>
  <div class="authentication">
    <v-container class="pa-3" fluid>
      <v-row class="h-100vh d-flex justify-center align-center">
        <v-col class="d-flex align-center" cols="12" lg="4" xl="3">
          <v-card class="px-sm-1 px-0 withbg mx-auto" elevation="10" max-width="500" rounded="md">
            <v-card-item class="pa-sm-8">
              <div class="d-flex justify-center py-4">
                <Logo />
              </div>
              <div class="text-body-1 text-muted text-center mb-3">Your Social Campaigns</div>
              <LoginForm />
              <h6 class="text-h6 text-muted font-weight-medium d-flex justify-center align-center mt-3">
                New to Modernize?
                <RouterLink
                  class="text-primary text-decoration-none text-body-1 opacity-1 font-weight-medium pl-2"
                  :to="{ name: 'register' }"
                >
                  Create an account</RouterLink>
              </h6>
            </v-card-item>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
