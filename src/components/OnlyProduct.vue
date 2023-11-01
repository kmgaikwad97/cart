<template>
    <div>
        <div class="container product-page">
            <div class="row">
                <div class="col-5">
                    <img :src="imgLink" class="img-fluid" alt="">
                </div>
                <div class="col-7">
                    <p class="title">
                        <b>{{ name }}</b>
                    </p>
                    <div>
                        <p class="price">
                            <b>₹ {{ price }}</b>
                        </p>
                    </div>
                    <div>
                        <p>{{ description }}</p>
                    </div>
                    <button @click="addtocart(id)" type="button" class="btn btn-danger">Add to Cart</button>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
import axios from 'axios'
export default {
    name: 'OnlyProduct',
    data() {
        return {
            name: "",
            imgLink: "",
            price: "",
            description: "",
            id:""
        }
    },
    async mounted() {
        // Fetch product details using productId and set them to this.product
        // const productId = this.$route.params.id;
        // console.log("productId ::123::", productId);

        // Retrieve the token from local storage
        const token = localStorage.getItem('token');
        console.log("token ::", token);

        const pid = localStorage.getItem('id');
        console.log("id ::", pid);

        try {

            // Set the Authorization header in the Axios request
            const headers = {
                'Authorization': `Bearer ${token}`,
            };
            let result = await axios.get("http://localhost:4000/api/v1/product/" + pid, { headers });
            console.log("result :", result);
            // this.product = result.data
            // console.log(this.product.name);
            // console.log(this.product.price);
            if (result.data) {
            this.name = result.data.name
            this.imgLink = result.data.imgLink
            this.price = result.data.price
            this.description = result.data.description
            this.id = result.data._id
            }
        }
        catch (err) {
            console.log("err ::", err);
        }
    },
    methods: {
        async addtocart(id) {
            console.log("prerererer");
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
    },
}


</script>
  
<style></style>