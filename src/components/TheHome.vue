<template>
<div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <a class="navbar-brand" href="#">
            <h4>HOME</h4>
        </a>
          
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
            
            </ul>
    
            <div>
                <button 
                    class="btn btn-secondary " 
                    type="button" 
                    id="signOutButton" 
                    @click="logOut">
                    Log Out
                </button>
            
            </div>
        
        </div>
    </nav>

  <div class="container mt-3 col-md-5">
      <div class="card card-body">
        <h3>
            Datos de usuario
        </h3>
        <hr>
        <p>
            Nombre: {{ user.name }}
        </p>
        <p>
            Email: {{ user.email }}
        </p>
      </div>


  </div>
  
</div>
</template>

<script>
// @ is an alias to /src
import VueJwtDecode from 'vue-jwt-decode';

export default {
  data(){
    return{
        user: {}
    }
  },
  methods: {
    getUserDetails(){

        let token = localStorage.getItem('jwt');
        let user = VueJwtDecode.decode(token);

        if (token){
            this.user = user;
        }
    },
    logOut(){
        localStorage.removeItem('jwt');
        // localStorage.removeItem('user');

        this.$router.push('/');
    }
  },
  created(){
      this.getUserDetails();
  }
}
</script>
