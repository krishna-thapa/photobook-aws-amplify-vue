<template>
  <div
    class="min-h-screen flex items-center justify-center bg-gray-50 py-12 px-4 sm:px-6 lg:px-8"
  >
    <div class="max-w-md w-full space-y-8">
      <div>
        <img
          class="mx-auto h-12 w-auto"
          src="https://tailwindui.com/img/logos/workflow-mark-indigo-600.svg"
          alt="Workflow"
        />
        <h2 class="mt-6 text-center text-3xl font-extrabold text-gray-900">
          Sign in to your account
        </h2>
      </div>
      <form
        class="flex flex-col items-center mt-8 space-y-6"
        @submit.prevent="login"
      >
        <div class="flex flex-col user">
          <label
            class="block text-gray-700 text-sm font-bold mb-2"
            for="userName"
            >User Name</label
          >
          <input
            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-md"
            type="text"
            placeholder="User name"
            v-model="username"
            id="userName"
          />
        </div>
        <div class="flex flex-col mt-10">
          <label
            class="block text-gray-700 text-sm font-bold mb-2"
            for="password"
            >Password</label
          >
          <input
            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-md"
            type="password"
            placeholder="Password"
            v-model="password"
          />
        </div>

        <div class="flex items-center justify-between">
          <div class="flex items-center">
            <input
              id="remember_me"
              name="remember_me"
              type="checkbox"
              class="h-4 w-4 text-indigo-600 focus:ring-indigo-500 border-gray-300 rounded"
            />
            <label for="remember_me" class="ml-2 block text-sm text-gray-900">
              Remember me
            </label>
          </div>

          <div class="text-sm px-3">
            <a
              href="#"
              class="font-medium text-indigo-600 hover:text-indigo-500"
            >
              Forgot your password?
            </a>
          </div>
        </div>

        <!-- eslint-disable -->
        <button class="btn-blue">Sign in</button>
      </form>
      <div class="text-red-600">{{ error.message }}</div>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";

export default {
  data: () => ({
    username: "",
    password: "",
    email: "",
    error: "",
  }),
  methods: {
    ...mapActions({
      loginVue: "auth/login",
    }),
    async login() {
      try {
        await this.loginVue({
          username: this.username,
          password: this.password,
        });
      } catch (error) {
        this.error = error;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
</style>