<script setup>
    import {
        ref,
        reactive,
        computed
} from 'vue'

const activeClass = ref('login');
let pass1 = ref('');
let pass2 = ref('');
const credentials = reactive([]);

import backImage from '../src/assets/thumbnail.png'

async function checkRegistration(p1, p2, u, f) {

  if (p1 == p2) {
    if (p1 == '' && p2 == '') {
      activeClass.value = 'emptypass';
    } else if (u == '') {
      activeClass.value = 'emptyusername';
    } else if (credentials.find(c => c.username === u)) {
      activeClass.value = 'notUnique';
    } else {
      credentials.push({ username: u, password: p1, fullname: f });
      activeClass.value = 'logout';
    }
  } else {
    activeClass.value='missmatch'
  }
  console.log(credentials);
  
}

function checkLogin(p, u) {
  
  const checkUser = credentials.find(user => user.username === u);
  const checkPass = credentials.find(user => user.password === p);
  if (checkUser && checkPass) {
    activeClass.value = 'logout';
      let user = ref(checkUser.username);
      let fullname = ref(checkUser.fullname);
  } else {
    activeClass.value = 'notMatched';
  }
}


</script>

<template>
    <section v-if="'logout'!=activeClass" class="flex items-center justify-center min-h-screen bg-gradient-to-r from-blue-500 to-cyan-500">
        
        <div class="grid lg:grid-cols-2" v-if="'login'==activeClass || 'notMatched'==activeClass">

            <div class="w-full flex flex-col justify-center items-center">
                    
                    <div class="w-full max-w-xs">
                        <h1 v-if="'notMatched'==activeClass" class="p-2 rounded text-xl font-semibold bg-red-500 mb-4 text-center text-white ">credential does not match !!</h1>
                        <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
                            <h2 class="py-4 mb-5 text-3xl font-semibold text-indigo-500">Login Form</h2>
                            <div class="mb-4">
                                <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
                                    Username
                                </label>
                                <input v-model="user"
                                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                                    id="username" type="text" placeholder="Username">
                            </div>
                            <div class="mb-6">
                                <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
                                    Password
                                </label>
                                <input v-model="pass"
                                    class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
                                    id="password" type="password" placeholder="******************">
                            </div>
                            <div class="flex items-center justify-between">
                                <button @click="checkLogin(pass,user)"
                                    class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                                    type="button">
                                    Sign In
                                </button>
                                <a @click="activeClass='register'" class="inline-block align-baseline font-bold text-sm text-orange-600 hover:text-orange-800"
                                    href="#">
                                    Or Register
                                </a>
                            </div>
                        </form>
                    </div>
            </div>

            <div class="">
                <div class="w-full object-cover object-center">
                    <img class="h-full w-full" src="https://i.ibb.co/KwYyNM8/thumbnail.png" alt="">
                </div>
            </div>
        </div>


        <div class="grid lg:grid-cols-2" v-if="'register'==activeClass || 'missmatch'==activeClass || 'emptypass'==activeClass || 'notUnique'==activeClass">
            <div  class=" w-full flex flex-col justify-center items-center ">
            <h2 class="my-5 text-3xl font-semibold text-white">Registration Form</h2>
            <div class="w-full max-w-xs">
              <h1 v-if="'missmatch'==activeClass" class="p-2 rounded text-xl font-semibold bg-red-500 mb-4 text-center text-white ">confirmation password does not match !!</h1>
              <h1 v-if="'emptypass'==activeClass" class="p-4 rounded bg-red-500 font-bold text-white m-4">passwords cannot be empty !!</h1>
              <h1 v-if="'emptyusername'==activeClass" class="p-4 rounded bg-red-500 font-bold text-white m-4">username cannot be empty !!</h1>
              <h1 v-if="'notUnique'==activeClass" class="p-4 rounded bg-red-500 font-bold text-white m-4">username has already been taken !!</h1>
                <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
                    <div class="mb-4">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
                            Fullname
                        </label>
                        <input v-model="fullname"
                            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                            id="username" type="text" placeholder="Username">
                    </div>
                    <div class="mb-4">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
                            Username
                        </label>
                        <input v-model="username"
                            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                            id="username" type="text" placeholder="Username">
                    </div>
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
                            Password
                        </label>
                        <input v-model="pass1"
                            class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
                            id="password" type="password" placeholder="******************">
                        <!-- <p class="text-red-500 text-xs italic">Please choose a password.</p> -->
                    </div>
                    <div class="mb-6">
                        <label class="block text-gray-700 text-sm font-bold mb-2" for="password">
                            Confirm Password
                        </label>
                        <input v-model="pass2"
                            class="shadow appearance-none border  rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
                            id="password" type="password" placeholder="******************">
                        <!-- <p class="text-red-500 text-xs italic">Please choose a password.</p> -->
                    </div>
                    <div class="flex items-center justify-between">
                        <button @click="checkRegistration(pass1,pass2,username,fullname)"
                            class="bg-orange-600 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                            type="button">
                            Register
                        </button>
                        <a @click="activeClass='login'" class="inline-block align-baseline font-bold text-sm text-orange-600 hover:text-orange-800"
                            href="#">
                            Or sign in
                        </a>
                        
                    </div>
                </form>  
            </div>  
            </div>

            <div class="flex justify-center items-center ">
                <img class="lg:w-full w-3/4" src="https://i.ibb.co/KwYyNM8/thumbnail.png" alt="">
            </div>
        </div>
        <!-- <template v-if="'logout' == activeClass">
              <div class="w-1/2 flex flex-col justify-center items-center bg-gray-200">
                <div class="p-4 mb-4 bg-white rounded">Welcome</div>
                <h1>Hi {{ user }}, you have Logged in !!</h1>
                <button @click="activeClass='login'" class="text-white mt-3 px-6 py-3 bg-red-500 hover:bg-red-700 rounded font-bold focus:outline-none focus:shadow-outline">Log Out</button>
              </div>
        </template> -->
    </section>
    <section v-if="'logout' == activeClass" class="flex h-screen w-full content-center">
        <div class="w-full flex flex-col items-center justify-center "
            style="background-image: url(https://cdn.pixabay.com/photo/2016/02/13/12/26/aurora-1197753_1280.jpg); background-repeat: no-repeat; background-size: cover;">
            <h1 class="mb-5 text-2xl mt-10 ml-10 text-white text-center">Welcome {{ fullname }} !!, you have Logged in.</h1>
            <button @click="activeClass='login'" class="text-center text-white mt-3 px-6 py-3 bg-red-500 hover:bg-red-700 rounded font-bold focus:outline-none focus:shadow-outline">Log Out</button>
        </div>
    </section>
</template>
<style scoped>
</style>