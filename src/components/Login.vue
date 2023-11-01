<template>
    <div>
      <div class="container">
        <div class="min-width-data">
          <form ref="anyName" @submit.prevent="postData" method="post">
            <div class="mb-3">
              <label for="exampleInputEmail1" class="form-label">Email address</label>
              <input type="name" v-model="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
              <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
            </div>
            <div class="mb-3">
              <label for="exampleInputPassword1" class="form-label">Password</label>
              <input type="password" v-model="password" class="form-control" id="exampleInputPassword1">
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
    name: 'Login',
    data() {
      return {
        posts: {
          email: "",
          password: "",
        }
      };
    },
    methods: {
      async postData() {
  
        const posts = {
          "email": this.email,
          "password": this.password,
        }
  
        let result = await axios.post(
          `http://localhost:4000/api/v1/login/`, posts
        )
        console.log(result);    

        // Check if the response contains a token
        const token = result.data.token;
        console.log("token :123:",token);
        if (token) {
          // Store the token in local storage
          localStorage.setItem('token', token);
          console.log('Token stored in local storage.',token);
        }
        this.$router.push({
        name: "Products",
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
  