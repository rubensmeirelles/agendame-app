<script setup lang="ts">
  import Logo from '@/layouts/full/logo/Logo.vue';
  /* Login form */
  import LoginForm from '@/components/auth/LoginForm.vue';

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
            </v-card-item>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
