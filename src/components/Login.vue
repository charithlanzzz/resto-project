<template>
  <section class="vh-100">
    <div class="container-fluid">
      <div class="row">
        <div class="col-sm-6 text-black">
          <div class="px-5 ms-xl-4">
            <img
              alt="SignUp"
              src="../assets/restu.png"
              style="width: 160px; height: 130px; margin-right: 40px;"
            />
          </div>

          <div class="d-flex align-items-center h-custom-2 px-5 ms-xl-4 mt-5 pt-5 pt-xl-0 mt-xl-n5">
            <form style="width: 25rem; margin-left: 50px;">
              <h1 class="fw-normal mb-3 pb-3" style="letter-spacing: 1px">
                Log in
              </h1>

              <div class="form-outline mb-4">
                <label class="form-label" for="form2Example18"
                  >Email address</label
                >
                <input
                  v-model="email"
                  type="email"
                  id="form2Example18"
                  class="form-control form-control-lg"
                  required
                />
              </div>

              <div class="form-outline mb-4">
                <label class="form-label" for="form2Example28">Password</label>
                <input
                  v-model="password"
                  type="password"
                  id="form2Example28"
                  class="form-control form-control-lg"
                  required
                />
              </div>

              <div class="pt-1 mb-4">
                <button v-on:click="login" class="btn btn-success">
                  Login
                </button>
              </div>

              <p class="small mb-5 pb-lg-2">
                <a class="text-muted" href="#!">Forgot password?</a>
              </p>
              <p>
                Don't have an account?
                <router-link to="/sign-up">Sign Up</router-link>
              </p>
            </form>
          </div>
        </div>
        <div class="col-sm-6 px-0 d-none d-sm-block">
          <img
            src="https://cdn.vox-cdn.com/thumbor/OheW0CNYdNihux9eVpJ958_bVCE=/0x0:5996x4003/1200x900/filters:focal(1003x1633:1961x2591)/cdn.vox-cdn.com/uploads/chorus_image/image/51830567/2021_03_23_Merois_008.30.jpg"
            alt="Login image"
            class="w-100 vh-100"
            style="object-fit: cover; object-position: left"
          />
        </div>
      </div>
    </div>
  </section>

  <!-- <div class="login">
        <label>Email:</label>
        <input type="text" v-model="email" placeholder="Enter the email"/><br>

        <label>Password:</label><br>
        <input type="text" v-model="password" placeholder="Enter the password"/><br>

        <button v-on:click="login" class="btn btn-success">Login</button>
        <p>
            <router-link to="/sign-up">Sign Up</router-link>
        </p>
    </div> -->
</template>

<script>
import axios from "axios";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Login",

  data() {
    return {
      email: "",
      password: "",
    };
  },

  methods: {
    async login() {
      let result = await axios.get(
        `http://localhost:3000/user?email=${this.email}&password=${this.password}`
      );

      if (result.status == 200 && result.data.length > 0) {
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "Home" });
      }

      console.warn(result);
    },
  },

  mounted() {
    let user = localStorage.getItem("user-info");
    if (user) {
      this.$router.push({ name: "Home" });
    }
  },
};
</script>
