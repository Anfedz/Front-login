
<template>
  <div class="wrapper fadeInDown">
    <div id="formContent">
      

      <form
        class="text-center p-5"
        style=""
        @submit.prevent="loginUser"
      ><div class="fadeIn first">
        <img src="@/assets/img/user.png" alt="icono de usuario">
      </div>
        <input
          type="text"
          id="email"
          class="fadeIn second"
          placeholder="Email"
          v-model="login.email"
        />
        <!-- Password -->
        <input
          type="password"
          id="password"
          class="fadeIn third"
          placeholder="Contraseña"
          v-model="login.password"
        />
        <!-- inicio sesion button -->
        
          <button type="submit" class="fadeIn fourth">
            Iniciar sesion
          </button>
        
      </form>
    </div>
  </div>
</template>
<script>
import swal from "sweetalert";
export default {
  data() {
    return {
      login: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    async loginUser() {
      try {
        let response = await this.$http.post("/api/auth/signin", this.login);
        console.log(response.data);
        let token = response.data.accessToken;
        localStorage.setItem("jwt", token);
        if (token) {
          swal("Exitoso", "login exitoso", "success");
          this.$router.push("/home");
        }
      } catch (err) {
        swal("Error", "datos incorrectos", "error");
        console.log(err.response);
      }
    },
  },
};
</script>
