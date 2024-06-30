<template>
    <div class="container">
        <div class="title-register-user">
            <h2>Criar Users</h2>
        </div>
        <div class="container-register-user">
            <form>
                <div class="row">
                    <div class="form-group col-md-6">
                        <input type="text" class="form-control input-register-user" v-model="name" name="name" id="name" aria-describedby="emailHelp" placeholder="Introduza um nome" />
                    </div>
                    <div class="form-group col-md-6">
                        <input type="text" class="form-control input-register-user" v-model="apelido" name="apelido"
                            id="apelido" placeholder="Introduza um apelido" />
                    </div>
                </div>
                <div class="row">
                    <div class="form-group col-md-12">
                        <input type="password" class="form-control input-register-user" v-model="pass" name="pass"
                            id="pass" aria-describedby="emailHelp" placeholder="Introduza uma password" />
                    </div>
                </div>
                <router-link to="/login-users" class="btn btn-outline-primary btn-register-user">Ir para o Login</router-link>
                <button type="button" @click='createUser()' class="btn btn-outline-success btn-register-user btn-right">Criar Conta</button>
            </form>
        </div>
    </div>
</template>

  
<script>

export default {
    name: 'CreateUser',
    data() {
        return {
            name: '',
            apelido: '',
            pass: ''
        }
    },
    methods: {
        createUser() {
            if (!this.name || !this.apelido || !this.pass) {
                alert("dados incompletos ");
                return;
            }
            const payload = {
                name: this.name,
                apelido: this.apelido,
                pass: this.pass,
                loggedIn: false
            }
            this.$emit('createUser', payload);
            this.clearForm();

            this.$router.push('/users'); 
        },
        clearForm() {
            this.name = "";
            this.apelido = "";
            this.pass = "";
        }
    }
}
</script>
  