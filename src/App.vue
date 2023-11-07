<template>
  <div id="app">
    <nav>
      <ProgressBar/>
      <router-link to="/">Register</router-link> |
      <router-link to="/login">Login</router-link> |
      <router-link to="/products">Products</router-link> |
      <router-link to="/cart">Cart</router-link> | 
      <router-link to="/address">Address</router-link> 
    </nav>
    <router-view/>
  </div>
</template>
<script>
import ProgressBar from './components/ProgressBar.vue';

export default {
    name: 'App',
    components: {
        ProgressBar
    },
    data() {
        return {
            userName: ""
        }
    },
    async mounted() {
      const token = localStorage.getItem('token');
      console.log("token ::", token);

        // Retrieve the token from local storage

        // const result = await axios.get('http://localhost:3001/getProduct');
        const result = await axios.get('http://localhost:4000/api/v1/',
        );
        console.log(result);
        this.product = result.data
    },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
