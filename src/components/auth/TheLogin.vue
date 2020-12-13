<template>
    <!-- Vista del login -->
    <div class="col-md-3">        
        <div class="card">

            <div class="card-header bg-primary"> 
                <h5 class="text-white mb-0">
                    {{ msg }}
                </h5>
            </div>

            <div class="card-body">
                <form>
                    <div class="form-group text-left">
                        <label for="exampleInputEmail1">
                            <b> Email address </b>
                            </label>
                        <input
                            type="email"
                            class="form-control"
                            id="exampleInputEmail1"
                            aria-describedby="emailHelp"
                            placeholder="Enter email"
                            v-model="login.email"
                        />
                    </div>
                    <div class="form-group text-left">
                        <label for="exampleInputPassword1">
                            <b> Password </b>
                            </label>
                        <input
                            type="password"
                            class="form-control"
                            id="exampleInputPassword1"
                            placeholder="Password"
                            v-model="login.password"
                        />
                    </div>

                    <pre>
                        {{ login }}
                    </pre>

                    <button 
                        type="submit" 
                        class="btn btn-primary btn-block"
                        @click.prevent="loginUser"
                        > Sign in
                    </button>
                </form>
            </div>
        </div> 
    </div>
</template>

<script>

import swal from 'sweetalert';

export default {
    name: 'TheLogin',
    props: {
    msg: String
    },
    data(){
        return{
            login: {
                email: '',
                password: ''
            }
        }
    },
    methods: {
        async loginUser(){
          try{
            let response = await this.$http.post('/api/auth/signin', this.login);
            console.log(response.data);

            let token = response.data.accessToken;
            // let user = response.data.user;

            localStorage.setItem('jwt', token);
            // localStorage.setItem('user', JSON.stringify(user));

            if (token){
              swal("Éxito!", "Login Correcto", "success");
              this.$router.push('/home');
            } 
        } catch(e) {
          swal("Oops!", "Usuario o contraseña incorrectos", "error");
          console.log(e);
          }
      }
    }
};

</script>

<style scoped>
label{
    font-size: 11pt;
}
</style>