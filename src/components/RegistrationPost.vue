<script setup lang="ts">
import { ref } from 'vue'

const username = ref<string>("");
const password = ref<string>("");


const registerForm = () => {
    fetch('http://localhost:1234/signup/',{
    method:  'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      'username': username.value,
      'password': password.value
    })
  })
}

const logInForm = () => {
    fetch('http://localhost:1234/login/',{
        method:  'POST',
        headers: {
        'Content-Type': 'application/json'
        },
        body: JSON.stringify({
        'username': username.value,
        'password': password.value
        })
    })
    .then(response => response.json())
    .then(data => localStorage.setItem("user", data.token))
}
</script>


<template>
    <div>
        <div>
            <p>{{username}}</p>
            <p>{{password}}</p>
        </div>
        <div>
            <p>
                Username:
            </p>
                <input type="text" placeholder="username" v-model="username"/>
        </div>
        <div>
        <p>
            Password:
        </p>
            <input type="text" placeholder="********" v-model="password"/>
        </div>
        <div>
            <button @click="registerForm">Register</button> <button @click="logInForm">Log In</button>
        </div>
    </div>

</template>


<style>
div{
    text-align: left;
    padding: 5px;
}
</style>