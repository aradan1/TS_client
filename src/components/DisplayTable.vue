<script setup lang="ts">
import { ref, onMounted } from 'vue'

const users = ref();

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
        },
    })
    .then(response => response.json())
    .then(data => users.value = data).then(() => console.log(users.value));
}

const editUser = (index: Number) => {
    fetch('http://localhost:1234/', {
        method: 'GET',
        headers: {
            accept: 'application/json',
        },
    })
    .then(response => response.json())
    .then(data => users.value = data).then(() => console.log(users.value));
}

</script>

<template>

    <div>
        <table>
            <tr>
                <th>ID</th>
                <th>USER</th>
                <th></th>
            </tr>
            <tr v-for="user in users" :key="user.id">
                <td>{{ user.id }}</td>
                <td>{{ user.username}}</td>
                <td><button @click="deleteUser(user.id)">delete</button> <button>Edit</button></td>
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
