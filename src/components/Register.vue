<template>
  <div>
    <div class="container">
      <div class="min-width-data">
        <form ref="anyName" @submit.prevent="postData" method="post">
          <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label">Name</label>
            <input type="name" v-model="name" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
            <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
          </div>
          <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label">Email address</label>
            <input type="name" v-model="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
            <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
          </div>
          <div class="mb-3">
            <label for="exampleInputPassword1" class="form-label">Password</label>
            <input type="password" v-model="password" class="form-control" id="exampleInputPassword1">
          </div>
          <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label">confirm password</label>
            <input type="password" v-model="confirmpassword" class="form-control" id="exampleInputEmail1"
              aria-describedby="emailHelp">
            <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
          </div>
          <div class="mb-3 form-check">
            <input type="checkbox" class="form-check-input" id="exampleCheck1">
            <label class="form-check-label" for="exampleCheck1">Check me out</label>
          </div>
          <button type="submit" class="btn btn-primary">Submit</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Register',
  data() {
    return {
      posts: {
        name: "",
        password_confirmation: "",
        email: "",
        password: "",
        tc: ""
      }
    };
  },
  methods: {
    async postData() {

      const posts = {
        "name": this.name,
        "email": this.email,
        "password": this.password,
        "password_confirmation": this.confirmpassword
      }

      let result = await axios.post(
        `http://localhost:4000/api/v1/register/`, posts
      )
      console.log(result);
      this.$router.push({
        name: "Login",
      });
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.min-width-data {
  margin: 0 30%;
}

h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
