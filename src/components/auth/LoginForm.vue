<template>
  <v-alert v-if="feedbackMessage" class="mb-2" color="error">{{ feedbackMessage }}</v-alert>
  <v-form @submit.prevent="submit">
    <v-row class="d-flex mb-3">
      <v-col cols="12 font-weight-bold mb-1"><v-label>E-mail</v-label>
        <v-text-field v-model="email" color="primary" :error-messages="errors.email" variant="outlined" />
      </v-col>
      <v-col cols="12">
        <v-label class="font-weight-bold mb-1">Senha</v-label>
        <v-text-field v-model="password" color="primary" :error-messages="errors.password" type="password"
          variant="outlined" />
      </v-col>
      <v-col class="pt-0" cols="12">
        <div class="d-flex flex-wrap align-center">
          <div class="ml-sm-auto">
            <RouterLink class="text-primary text-decoration-none text-body-1 opacity-1 font-weight-medium" to="/">
              Esqueceu sua senha?</RouterLink>
          </div>
        </div>
      </v-col>
      <v-col class="pt-0" cols="12">
        <v-btn block color="primary" flat size="large" type="submit" :loading="isSubmitting">Entrar</v-btn>
      </v-col>
    </v-row>
    <div>
      <h6 class="text-h6 text-muted font-weight-medium d-flex justify-center align-center mt-3">
        Novo no AgendaMe?
        <RouterLink class="text-primary text-decoration-none text-body-1 opacity-1 font-weight-medium pl-2"
          :to="{ name: 'register' }">
          Crie sua conta</RouterLink>
      </h6>
    </div>
  </v-form>
</template>

<script setup>
import { ref } from 'vue';
import axios from '@/plugins/axios';
import { useForm, useField } from 'vee-validate';
import { object, string } from 'yup';
import { useRouter } from 'vue-router';
import { useAuthStore } from '@/stores/auth';

const schema = object({
  email: string().required().email().label('E-mail'),
  password: string().required().label('Senha'),
})

const { handleSubmit, errors, isSubmitting } = useForm({
  validationSchema: schema
})

const submit = handleSubmit(async (values) => {
  await login(values)
})

const { value: email } = useField('email')
const { value: password } = useField('password')

const feedbackMessage = ref('');

const authStore = useAuthStore()

const router = useRouter();

function login(values) {
  feedbackMessage.value = '';

  authStore
    .sanctum()
    .then(() => {
      authStore
        .login(values.email, values.password)
        .then(() => {
          router.push({ name: 'dashboard' })
        }).catch(() => {
          feedbackMessage.value = 'E-mail ou senha inválidos!'
        })
    })
}

</script>
