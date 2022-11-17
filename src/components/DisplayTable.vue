<script setup lang="ts">
import { ref, onMounted } from 'vue'

const users = ref();
const editName = ref<string>("");

onMounted(() => {
    fetch('http://localhost:1234/', {
      method: 'GET',
      headers: {
        accept: 'application/json',
        
      },})
        .then(response => response.json())
        .then(data => users.value = data).then(() => console.log(users.value));
})

const deleteUser = (index: Number) => {
    fetch(`http://localhost:1234/${index}`, {
        method: 'DELETE',
        headers: {
            accept: 'application/json',
            Authorization: 'Bearer ' + localStorage.getItem('user')
        },
    })
    .then(response => response.json())
    .then(data => console.log(data));
}

const editUser = (index: Number) => {
    fetch(`http://localhost:1234/${index}`, {
        method: 'PUT',
        headers: {
            accept: 'application/json',
            'Content-Type': 'application/json',
            Authorization: 'Bearer ' + localStorage.getItem('user')
        },
        body: JSON.stringify({
            'username': editName.value
        })
    })
    .then(response => response.json())
    .then(data => console.log(data));
}

</script>

<template>

    <div>
        <div>
            <p>
                Edit username: 
                <input type="text" placeholder="username" v-model="editName"/>
            </p>
        </div>
        <table>
            <tr>
                <th>ID</th>
                <th>USER</th>
                <th></th>
            </tr>
            <tr v-for="user in users" :key="user.id">
                <td>{{ user.id }}</td>
                <td>{{ user.username}}</td>
                <td><button @click="deleteUser(user.id)">delete</button> <button @click="editUser(user.id)">Edit</button></td>
            </tr>
        </table>
    </div>

</template>

<style>
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td, th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}

</style>
