<template>
    <div>
      <div class="container product-page">
          <div class="product-heading">
              <h2>Products</h2>
          </div>
          <div class="row m-0">
              <div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2" v-for="items of product" :key="items._id">
                  <figure>
                      <img :src="items.imgLink" class="img-fluid" alt="">
                  </figure>
                  <p class="title">
                     <b>{{items.name}}</b> 
                  </p>
                  <div>
                      <p class="price">
                         <b>₹ {{items.price}}</b> 
                      </p>
                  </div>
                  <div>
                      <p>{{items.description}}</p>
                  </div>
                  <button  @click="addtocart(items._id)" type="button" class="btn btn-danger">Add To Cart</button>
              </div>
          </div>
  
          <!-- pagination starts -->
  
          <div class="my-4">
              <h2>Pagination coming soon</h2>
          </div>
          <!-- pagination ends -->
  
  
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios'
  export default {
      name:'Cart',
      data(){
          return{
              product:""
          }
      },
      async mounted() {
        const token = localStorage.getItem('token');
            console.log("token ::", token);

            try{
                 // Set the Authorization header in the Axios request
                 const headers = {
                    'Authorization': `Bearer ${token}`,
                };
                let result = await axios.get("http://localhost:4000/api/v1/getCart/", { headers });
                console.log("result :", result);
                this.product = result.data
            }catch(err){
                console.log(err.message);
            }
      },
    //   methods: {
    //   // async getAll() {
    //   //   const result = await axios.get("http://localhost:3001/user");
    //   //   console.log("result", result.data);
    //   //   this.user = result.data;
    //   // },
    //   async addtocart(id) {
    //     console.log("id", id);
    //     let result = await axios.post("http://localhost:4000/api/v1/addtocart/" + id);
    //   //   this.getAll();
    //     console.log("result :",result);
    //   },
    // },
  }
  
  
  </script>
  
  <style>
  
  </style>