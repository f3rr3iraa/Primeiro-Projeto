<template>
  <Navbar />
  <div class="container">
    <PushUsers :numberOfUsers="numberOfUsers" @getAllUsers="getAllUsers()" />
    <div class="container-board-users">
      <h2>Users</h2>
    </div>
    <table class="table table-bordered">
      <thead>
        <tr>
          <th>Nome</th>
          <th>Apelido</th>
          <th>Password</th>
          <th>Authenticated</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in users" :key="item.name">
          <td>{{ item.name }}</td>
          <td>{{ item.apelido }}</td>
          <td>{{ item.pass }}</td>
          <td>{{ isAuthenticated(item.name, item.apelido) }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Navbar from './Navbar.vue'
import PushUsers from './PushUsers.vue'
import { getAllUsers } from '../services/UserService'

export default {
  name: 'Users',
  props: ['users'],
  components: {
    Navbar,
    PushUsers
  },
  data() {
    return {
      users: [],
      numberOfUsers: 0
    }
  },
  methods: {
    getAllUsers() {
      getAllUsers().then(response => {
        console.log(response)
        this.users = response
        this.numberOfUsers = this.users.length
      })
    },
    isAuthenticated(name, apelido) {
      const loggedInUser = this.users.find(user => user.name === name && user.loggedIn);
      return loggedInUser ? 'Logado' : 'nao Logado';
    }
  },
  computed: {
    totalAuthenticatedUsers() {
      return this.users.filter(user => user.loggedIn).length;
    }
  },
  mounted() {
    this.getAllUsers();
  }
}
</script>
