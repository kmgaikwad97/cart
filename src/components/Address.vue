<template>
    <div>
        <div class="container">
            <div class="row">
                <div class="col-12 col-md-9">
                    <div class="border p-3">
                        <div class="address-add text-start py-2 pr-2">
                            <i class="fa-solid fa-plus" data-bs-toggle="modal" data-bs-target="#exampleModal"
                                data-bs-whatever="@mdo"></i> Add Address
                        </div>
                        <h4 class="text-start">Select a Delivery Address</h4>
                        <div class="text-start d-flex align-items-baseline" v-for="(address, index) in add" :key="index">
                            <input type="radio" :id="'address_' + index" :value="address" v-model="selectedAddress" />
                            <label class="ps-3" :for="'address_' + index">
                                <strong class="text-capitalize"><b>{{ address.fullname }}</b></strong> - {{ address.flat }},
                                {{ address.area }},
                                {{ address.area }},
                                {{ address.landmark }},
                                {{ address.city }},
                                {{ address.state }}, {{ address.pincode }}, {{ address.country }}
                            </label>
                        </div>
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
                        <button type="button" @click="submitAddress" class="my-3 btn btn-success">Proceed to Buy</button>
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



        <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <h1 class="modal-title fs-5" id="exampleModalLabel">Add a New Address</h1>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        <form ref="anyName">
                            <div class="mb-3 d-flex flex-column">
                                <label for="recipient-country" class="col-form-label" id="country">Country</label>
                                <select v-model="country" id="country">
                                    <option v-for="country in countries" :key="country.code" :value="country.code">
                                        {{ country.name }}
                                    </option>
                                </select>
                            </div>
                            <div class="mb-3">
                                <label for="name" class="col-form-label">Name</label>
                                <input v-model="fullname" type="text" class="form-control" id="name">
                            </div>
                            <div class="mb-3">
                                <label for="mobile" class="col-form-label">Mobile Number</label>
                                <input v-model="mobile" type="text" class="form-control" id="mobile">
                            </div>

                            <div class="mb-3">
                                <label for="pincode" class="col-form-label">Pincode</label>
                                <input v-model="pincode" type="text" class="form-control" id="pincode">
                            </div>
                            <div class="mb-3">
                                <label for="address" class="col-form-label">Flat, House no., Building, Company,
                                    Apartment</label>
                                <input v-model="flat" type="text" class="form-control" id="address">
                            </div>
                            <div class="mb-3">
                                <label for="pincode" class="col-form-label">Area, Street, Sector, Village</label>
                                <input v-model="area" type="text" class="form-control" id="pincode">
                            </div>
                            <div class="mb-3">
                                <label for="landmark" class="col-form-label">Landmark</label>
                                <input v-model="landmark" type="text" class="form-control"
                                    placeholder="eg. near rajyog hotel" id="landmark">
                            </div>
                            <div class="row">
                                <div class="col-6">
                                    <div class="mb-3">
                                        <label for="city" class="col-form-label">Town/City</label>
                                        <input v-model="city" type="text" class="form-control"
                                            placeholder="eg. near rajyog hotel" id="city">
                                    </div>
                                </div>
                                <div class="col-6">
                                    <div class="mb-3">
                                        <label for="state" class="col-form-label">State</label>
                                        <input v-model="state" type="text" class="form-control"
                                            placeholder="eg. near rajyog hotel" id="state">
                                    </div>
                                </div>
                            </div>
                        </form>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                        <button @click="postData" type="button" data-bs-dismiss="modal" class="btn btn-primary">Use this
                            Address</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
import axios from 'axios'
// import $ from 'jquery'; // Import jQuery

export default {
    name: 'Address',
    data() {
        return {
            selectedAddress: null,
            add: [],
            address: {
                country: null,
                fullname: "",
                mobile: "",
                pincode: "",
                flat: "",
                area: "",
                landmark: "",
                city: "",
                state: "",
            },
            // selectedCountry: null,
            countries: [
                { code: 'IN', name: 'India' },
                { code: 'US', name: 'United States' },
                { code: 'CA', name: 'Canada' },
                { code: 'UK', name: 'United Kingdom' },
                // Add more countries as needed
            ],
        };
    },
    async mounted() {
        // Log the selected address ID
        // console.log('Selected Address ID:', this.selectedAddressId);
        // // Retrieve the token from local storage
        // const token = localStorage.getItem('token');
        // console.log("token ::", token);
        // try {

        //     // Set the Authorization header in the Axios request
        //     const headers = {
        //         'Authorization': `Bearer ${token}`,
        //     };
        //     let result = await axios.get("http://localhost:4000/api/v1/getUsersAddress/", { headers });
        //     console.log('Selected Address ID:', this.selectedAddressId);
        //     console.log("result :", result);
        //     this.add = result.data.addresses
        //     console.log("this.address ::", this.add);
        // }
        // catch (err) {
        //     console.log("err ::", err);
        // }
        await this.fetchAddresses()

    },
    methods: {
        async fetchAddresses() {
      const token = localStorage.getItem('token');
      try {
        const headers = {
          'Authorization': `Bearer ${token}`,
        };
        const result = await axios.get("http://localhost:4000/api/v1/getUsersAddress/", { headers });
        this.add = result.data.addresses;
        console.log("Updated Address List:", this.add);
      } catch (err) {
        console.log("Error fetching addresses:", err);
      }
    },
        submitAddress() {
            if (this.selectedAddress) {
                console.log("Selected Address:", this.selectedAddress._id);
            }
        },

        async postData() {
            // Log the selected address ID
            console.log("pressed");
            const token = localStorage.getItem('token');
            console.log("token ::", token);

            let address = {
                "country": this.country,
                "fullname": this.fullname,
                "mobile": this.mobile,
                "pincode": this.pincode,
                "flat": this.flat,
                "area": this.area,
                "landmark": this.landmark,
                "city": this.city,
                "state": this.state,
            }
            console.log("address ::", address);
            try {

                // Set the Authorization header in the Axios request
                const headers = {
                    'Authorization': `Bearer ${token}`,
                };
                let result = await axios.post("http://localhost:4000/api/v1/address/", address, { headers });
                this.$refs.anyName.reset();
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