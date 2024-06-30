<template>
    <Navbar />
    <div class="container">
        <div class="title-register-user">
            <h2>Login Users</h2>
        </div>
        <div class="container-login-users">
            <form>
                <div class="container-login-users">
                        <input type="text" class="form-control input-register-user" v-model="name" name="name" id="name" aria-describedby="emailHelp" placeholder="Introduza o nome" />
                </div>
                <div class="container-login-users">
                        <input type="password" class="form-control input-register-user" v-model="pass" name="pass" id="pass" aria-describedby="emailHelp" placeholder="Introduza a password" />
                </div>
                <router-link to="/" class="btn btn-outline-primary btn-register-user">Register</router-link>
                <button type="button" @click='loginUsers()' class="btn btn-outline-success btn-register-user btn-right">login</button>
            </form>
        </div>
    </div>
</template>
  
<script>
import Navbar from './Navbar.vue'
import { loginUsers } from '../services/UserService.js'
import router from '../router/routes.js'

export default {
    name: 'loginUsers',
    components: {
        Navbar
    },
    data() {
        return {
            name: '',
            pass: ''
        }
    },
    methods: {
    loginUsers() {
        if (!this.name || !this.pass) {
            alert("dados incompletos ");
            return;
        }
        const payload = {
            name: this.name,
            pass: this.pass,
        };
        loginUsers(payload)
            .then((response) => {
                if (response === "login com sucesso") {
                    console.log(payload.name);
                    localStorage.setItem("user", payload.name);
                    router.push({ name: "Users" });
                } else {
                    console.log(response);
                }
            })
            .catch((error) => {
                console.error(error);
            });
        this.clearForm();
    },
    clearForm() {
        this.name = "";
        this.pass = "";
    }
    }
}
</script>