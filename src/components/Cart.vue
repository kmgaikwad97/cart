<template>
    <div>
        <div class="container product-page">
            <div class="product-heading">
                <h2>Products</h2>
            </div>
            <div class="row m-0">
                <div class="row col-12 col-md-9">
                    <div class="col-12 p-5 d-flex align-items-center flex-column" v-for="items of product" :key="items._id">
                        <figure>
                            <img :src="items.imgLink" class="img-fluid" alt="">
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
                        <!-- <button @click="addtocart(items._id)" type="button" class="btn btn-danger">Add To Cart</button> -->
                    </div>
                </div>
                <div class="col-12 col-md-3">
                    <div class="total-cart border p-3">
                        <h5>Subtotal ({{ count }} item): {{ total }}</h5>
                        <div class="form-check">
                            <input class="form-check-input" type="checkbox" value="" id="flexCheckDefault">
                            <label class="form-check-label" for="flexCheckDefault">
                                This order contains a gift
                            </label>
                        </div>
                        <button type="button" class="my-3 btn btn-success">Proceed to Buy</button>
                        <div class="accordion" id="accordionExample">
                            <div class="accordion-item">
                                <h2 class="accordion-header">
                                    <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse"
                                        data-bs-target="#flush-collapseOne" aria-expanded="false"
                                        aria-controls="flush-collapseOne">
                                        EMI AVAILABLE
                                    </button>
                                </h2>
                                <div id="flush-collapseOne" class="accordion-collapse collapse"
                                    data-bs-parent="#accordionFlushExample">
                                    <div class="accordion-body">Your order qualifies for EMI with valid credit cards (not
                                        available on purchase of Gold, Jewelry, Gift cards and Amazon pay balance top up).
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>
  
<script>
import axios from 'axios'
export default {
    name: 'Cart',
    data() {
        return {
            product: "",
            count: '',
            total: ''
        }
    },
    async mounted() {
        const token = localStorage.getItem('token');
        console.log("token ::", token);

        try {
            // Set the Authorization header in the Axios request
            const headers = {
                'Authorization': `Bearer ${token}`,
            };
            let result = await axios.get("http://localhost:4000/api/v1/getCart/", { headers });
            console.log("result :", result);
            this.product = result.data.data
            this.count = result.data.count
            this.total = result.data.total
        } catch (err) {
            console.log(err.message);
        }
    },
}


</script>
  
<style>
figure {
    cursor: pointer;
    height: 200px;
    width: 200px;
}

figure img {
    max-width: 100%;
    height: 100%;
}

.accordion-button,
.accordion-button::after {
    font-size: 10px !important;
}

.accordion-body {
    font-size: 10px;

}
</style>