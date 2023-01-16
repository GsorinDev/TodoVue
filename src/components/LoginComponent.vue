<template>
  <section>
    <div v-if="!forgotPassword" class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0">
      <div class="w-full bg-white rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700">
        <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
          <h1 class="text-xl font-bold leading-tight tracking-tight text-gray-900 md:text-2xl dark:text-white">
            Sign in to your account
          </h1>
          <div v-if="errorBool" class="mb-6 w-full text-white bg-red-500 focus:outline-none font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-red-600">{{error}}</div>
          <form class="space-y-4 md:space-y-6">
            <div>
              <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your email</label>
              <input v-model="user.email" type="email" name="email" id="email" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="name@company.com" required="">
            </div>
            <div>
              <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Password</label>
              <input v-model="user.password" type="password" name="password" id="password" placeholder="••••••••" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required="">
            </div>
            <div class="flex items-center justify-end">
              <a @click="forgotPasswordFunction" class="text-sm font-medium text-blue-600 hover:underline dark:text-blue-500 cursor-pointer">Forgot password?</a>
            </div>
            <button v-on:click="verifyLogin" type="button" class="w-full text-white bg-blue-500 hover:bg-blue-700 focus:outline-none focus:ring-primary-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-primary-600 dark:hover:bg-primary-700 dark:focus:ring-primary-800">Sign in</button>
<!--            <p class="text-sm font-light text-gray-500 dark:text-gray-400">-->
<!--              Don’t have an account yet? <a href="#" class="font-medium text-primary-600 hover:underline dark:text-primary-500">Sign up</a>-->
<!--            </p>-->
          </form>
        </div>
      </div>
    </div>
    <div v-else class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0">
      <div class="w-full bg-white rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700">
        <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
          <h1 class="text-xl font-bold leading-tight tracking-tight text-gray-900 md:text-2xl dark:text-white">
            Rescue Account
          </h1>
          <div v-if="errorBool" class="mb-6 w-full text-white bg-red-500 focus:outline-none font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-red-600">{{error}}</div>
          <form class="space-y-4 md:space-y-6">
            <div  v-if="!code && !email">
              <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your email</label>
              <input v-model="rescue.email" type="email" name="email" id="email" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="name@company.com" required="">
            </div>
            <div v-else-if="!code && email">
              <label for="code" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your Code</label>
              <input v-model="rescue.code" type="text" name="code" id="code" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="your code" required="">
            </div>
            <div v-else>
              <div>
                <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Password</label>
                <input v-model="rescue.password" type="password" name="password" id="password" placeholder="••••••••" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required="">
              </div>
              <div>
                <label for="confirmPassword" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">confirm Password</label>
                <input v-model="rescue.confirmPassword" type="password" name="confirmPassword" id="confirmPassword" placeholder="••••••••" class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" required="">
              </div>
            </div>
            <div class="flex items-center justify-end">
              <a @click="forgotPasswordFunction" class="text-sm font-medium text-blue-600 hover:underline dark:text-blue-500 cursor-pointer">Login</a>
            </div>

            <button v-on:click="rescueAccount" type="button" class="w-full text-white bg-blue-500 hover:bg-blue-700 focus:outline-none focus:ring-primary-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-primary-600 dark:hover:bg-primary-700 dark:focus:ring-primary-800">
              {{ button }}</button>
            <!--            <p class="text-sm font-light text-gray-500 dark:text-gray-400">-->
            <!--              Don’t have an account yet? <a href="#" class="font-medium text-primary-600 hover:underline dark:text-primary-500">Sign up</a>-->
            <!--            </p>-->
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import _ from 'lodash'
import {store} from "@/store";
import {createLocalStorageVariable, removeLocalStorageVariable} from "@/assets/js/localStorage";

export default {
  name: "LoginComponent",
  computed: {
  },
  data:() => ({
    user: {email:"", password: ""},
    rescue: {email: "", code:"", password: "" , confirmPassword:""},
    errorBool : false,
    error : "",
    forgotPassword:false,
    code:false,
    email:false,
    button: "Send Mail"
  }),
  components: {
  },
  methods: {
    async verifyLogin(){
      if(this.user.email !== "" && this.user.password !== "") {
        await store.dispatch('login', this.user)
        removeLocalStorageVariable('token')
        const token =  _.get(await store.getters.getToken, 'message')
        if (token.startsWith("eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9")) {
          createLocalStorageVariable('token', token)
          this.$emit('menu', 'home')
        } else {
          this.errorBool = true
          this.error = token
          setTimeout(() => {this.errorBool = false}, 2000)
        }

      } else {
        this.errorBool = true
        this.error = "Veuillez remplir tout les champs"
        setTimeout(() => {this.errorBool = false}, 2000)
      }
    },
    forgotPasswordFunction(){
      this.forgotPassword = !this.forgotPassword
    },
    async rescueAccount(){
      if(!this.code && !this.email && this.rescue.email !== "") {
        await store.dispatch("sendEmail", {'email': this.rescue.email})
        this.email = await store.getters.getEmail
        this.button = "Send Code"
      }

      else if(!this.code && this.email && this.rescue.email !== "" && this.rescue.code !== "") {
        await store.dispatch("sendCode", {'email': this.rescue.email, 'code': this.rescue.code})
        this.code = await store.getters.getCode
        this.button = "Change password"
      }

      else if(this.code && this.email && this.rescue.email !== "" && this.rescue.code !== "" && this.rescue.password !== "" && this.rescue.password.length >= 6 && this.rescue.confirmPassword !== "" && this.rescue.confirmPassword.length >= 6 && this.rescue.password === this.rescue.confirmPassword) {
        await store.dispatch("changePassword", {'email': this.rescue.email, 'code': this.rescue.code, 'password': this.rescue.password})
        this.button = "Send Mail"
        this.code = false
        this.email = false
        this.$emit('menu', 'home')
      }

      else {
        this.errorBool = true
        this.error = "Veuillez remplir les différents champs correctement"
        setTimeout(() => {this.errorBool = false}, 2000)
      }
    }
  },
   mounted() {
  }
}
</script>

<style scoped>

</style>