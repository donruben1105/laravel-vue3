<script setup lang="ts">
import { RegisterPayload } from '@/types';
import type { FormKitNode } from '@formkit/core'

definePageMeta({
  layout: "centered",
  middleware: ['guest'],
});

const {register} = useAuth()

async function handleRegister (payload: RegisterPayload, node?: FormKitNode) {
  try {
    await register(payload)
  } catch (error) {
    handleInvalidForm(error, node)
  }
}
</script>
<template>
  <div class="register">
    <h1>Register</h1>
    <FormKit type="form" submit-label="Login" @submit="handleRegister">
      <FormKit label="Name" name="name" type="text" />
      <FormKit label="Email" name="email" type="text" />
      <FormKit label="password" name="password" type="password" />
      <FormKit label="password" name="password_confirmation" type="password" />
    </FormKit>
    <!-- <form @submit.prevent="register(form)">
      <label>
        <div>Name</div>
        <input v-model="form.name" type="text" />
      </label>

      <label>
        <div>Email</div>
        <input v-model="form.email" type="email" />
      </label>

      <label>
        <div>Password</div>
        <input v-model="form.password" type="password" />
      </label>

      <label>
        <div>Confirm Password</div>
        <input v-model="form.password_confirmation" type="password" />
      </label>

      <button class="btn">Register</button>
    </form> -->

    <p>
      Already have an account?
      <NuxtLink class="underline text-lime-600" to="/login">Login</NuxtLink>
    </p>
  </div>
</template>
