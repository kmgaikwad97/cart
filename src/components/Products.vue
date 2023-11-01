<template>
    <div>
        <div class="container product-page">
            <div class="product-heading">
                <h2>Products</h2>
            </div>
            <div class="row m-0">
                <div class="col-12 col-sm-6 col-md-4 col-lg-3 col-xl-2 p-5 d-flex align-items-center flex-column" v-for="items of product" :key="items._id">
                    <figure @click="onlyProduct(items._id)" >
                        <img :src="items.imgLink" alt="">
                    </figure>
                    <p class="title">
                        <b>{{ items.name }}</b>
                    </p>
                    <div>
                        <p class="price">
                            <b>₹ {{ items.price }}</b>
                        </p>
                    </div>
                    <div>
                        <p>{{ items.description }}</p>
                    </div>
                    <button @click="addtocart(items._id)" type="button" class="btn btn-danger">Add To Cart</button>
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
    name: 'Product',
    data() {
        return {
            product: ""
        }
    },
    async mounted() {
        // Retrieve the token from local storage

        // const result = await axios.get('http://localhost:3001/getProduct');
        const result = await axios.get('http://localhost:4000/api/v1/getAllProducts',
        );
        console.log(result);
        this.product = result.data
    },
    methods: {
        // async getAll() {
        //   const result = await axios.get("http://localhost:3001/user");
        //   console.log("result", result.data);
        //   this.user = result.data;
        // },
        async addtocart(id) {
            const token = localStorage.getItem('token');
            console.log("token ::", token);
            console.log("id", id);

            try {

                // Set the Authorization header in the Axios request
                const headers = {
                    'Authorization': `Bearer ${token}`,
                };
                let result = await axios.post("http://localhost:4000/api/v1/addtocart/" + id, null, { headers });
                //   this.getAll();
                console.log("result :", result);
            }
            catch (err) {
                console.log("err ::", err);
            }
        },

        async onlyProduct(id){
            // Check if the response contains a token
        if (id) {
          // Store the token in local storage
          localStorage.setItem('id', id);
          console.log('product id stored in local storage.',id);
        }
            // console.log("id", id);
            // const token = localStorage.getItem('token');
            // console.log("token ::", token);
            try{
                this.$router.push({
                    name: "Product",
                    params: { id } 
                });
            //     // Set the Authorization header in the Axios request
            //     const headers = {
            //       'Authorization': `Bearer ${token}`,
            //   };
            //   let result = await axios.get("http://localhost:4000/api/v1/product/" + id, { headers });
            //     // this.getAll();
            //   console.log("result :", result);

            }catch(err){
                console.log(err.message);
            }
        }
    }
}


</script>
  
<style>
figure{
    cursor: pointer;
    height: 200px;
    width: 200px;
}
figure img, .img-fluid{
    max-width: 100%;
    height: 100% !important;
}
</style>