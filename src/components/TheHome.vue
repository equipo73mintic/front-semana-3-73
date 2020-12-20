<template>
  <div>
    <nav class="navbar navbar-expand-lg" style="background-color: #4163c7">
      <a class="navbar-brand">
        <span style="color: #ffffff">HOME</span>
      </a>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto"></ul>

        <div>
          <button
            class="btn btn-secondary"
            type="button"
            id="signOutButton"
            style="background-color: #ece3e1"
            @click="logOut"
          >
            <span style="color: #4163c7">Logout</span>
          </button>
        </div>
      </div>
    </nav>

    <div class="container mt-3 col-md-5">
      <div class="card card-body">
        <h3>Bienvenido Usuario</h3>
        <hr />
        <div class="alert alert-primary" role="alert">
          <span> <strong>Nombre:</strong>  {{ user.name }}</span>
        </div>
        <div class="alert alert-primary" role="alert">
          <span> <strong>Email:</strong>  {{ user.email }}</span>
        </div>
           <div class="mt-2">
            <div class="d-flex justify-content-center links">
                Ciclo III - Grupo 73
            </div>
            <div class="d-flex justify-content-center links">
                <a
                href="https://github.com/equipo73mintic/Semana-3-73"
                target="_blank"
                >
                <i class="fab fa-github fa-fw Git-hub"> </i>
                </a>
            </div>
            </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import VueJwtDecode from "vue-jwt-decode";

export default {
  data() {
    return {
      user: {},
    };
  },
  methods: {
    getUserDetails() {
      let token = localStorage.getItem("jwt");
      let user = VueJwtDecode.decode(token);

      if (token) {
        this.user = user;
      }
    },
    logOut() {
      localStorage.removeItem("jwt");
      // localStorage.removeItem('user');

      this.$router.push("/");
    },
  },
  created() {
    this.getUserDetails();
  },
};
</script>
