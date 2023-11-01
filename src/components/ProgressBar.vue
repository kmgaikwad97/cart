<template>
  <div>
    <div class="main">

      <div class="head">
        <p class="head_1">Animated Step <span>Progress Bar</span></p>
        <p class="head_2">Using Html, Css & JavaScript</p>
      </div>

      <ul>  
        <li>
          <i class="icon uil uil-capture"></i>
          <div @click="activateStep(1)" :class="{ active: activeStep === 1}" class="progress one">
            <p>1</p>
            <i class="uil uil-check"></i>
          </div>
          <p class="text">Add To Cart</p>
        </li>
        <li>
          <i class="icon uil uil-clipboard-notes"></i>
          <div @click="activateStep(2)" :class="{ active: activeStep === 2}" class="progress two">
            <p>2</p>
            <i class="uil uil-check"></i>
          </div>
          <p class="text">Fill Details</p>
        </li>
        <li>
          <i class="icon uil uil-credit-card"></i>
          <div @click="activateStep(3)" :class="{ active: activeStep === 3}" class="progress three">
            <p>3</p>
            <i class="uil uil-check"></i>
          </div>
          <p class="text">Make Payment</p>
        </li>
        <li>
          <i class="icon uil uil-exchange"></i>
          <div @click="activateStep(4)" :class="{ active: activeStep === 4}" class="progress four">
            <p>4</p>
            <i class="uil uil-check"></i>
          </div>
          <p class="text">Order in Progr</p>
        </li>
        <li>
          <i class="icon uil uil-map-marker"></i>
          <div @click="activateStep(5)" :class="{ active: activeStep === 5}" class="progress five">
            <p>5</p>
            <i class="uil uil-check"></i>
          </div>
          <p class="text">Order Arrived</p>
        </li>
      </ul>

    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Product',
  data() {
    return {
      product: "",
      activeStep: 1,
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
    activateStep(step) {
      this.activeStep = step;
    },
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

    async onlyProduct(id) {
      // Check if the response contains a token
      if (id) {
        // Store the token in local storage
        localStorage.setItem('id', id);
        console.log('product id stored in local storage.', id);
      }
      // console.log("id", id);
      // const token = localStorage.getItem('token');
      // console.log("token ::", token);
      try {
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

      } catch (err) {
        console.log(err.message);
      }
    }
  }
}


</script>

<style>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
/* @font-face {
    font-family: pop;
    src: url(./Fonts/Poppins-Medium.ttf);
} */

.main{
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: pop;
    flex-direction: column;
}
.head{
    text-align: center;
}
.head_1{
    font-size: 30px;
    font-weight: 600;
    color: #333;
}
.head_1 span{
    color: #ff4732;
}
.head_2{
    font-size: 16px;
    font-weight: 600;
    color: #333;
    margin-top: 3px;
}
ul{
    display: flex;
    margin-top: 80px;
}
ul li{
    list-style: none;
    display: flex;
    flex-direction: column;
    align-items: center;
}
ul li .icon{
    font-size: 35px;
    color: #ff4732;
    margin: 0 60px;
}
ul li .text{
    font-size: 14px;
    font-weight: 600;
    color: #ff4732;
}

/* Progress Div Css  */

ul li .progress{
    width: 30px;
    height: 30px;
    border-radius: 50%;
    background-color: rgba(68, 68, 68, 0.781);
    margin: 14px 0;
    display: grid;
    place-items: center;
    color: #fff;
    position: relative;
    cursor: pointer;
}
.progress::after{
    content: " ";
    position: absolute;
    width: 125px;
    height: 5px;
    background-color: rgba(68, 68, 68, 0.781);
    right: 30px;
}
.one::after{
    width: 0;
    height: 0;
}
ul li .progress .uil{
    display: none;
}
ul li .progress p{
    font-size: 13px;
}

/* Active Css  */

ul li .active{
    background-color: #ff4732;
    display: grid;
    place-items: center;
}
li .active::after{
    background-color: #ff4732;
}
ul li .active p{
    display: none;
}
ul li .active .uil{
    font-size: 20px;
    display: flex;
}

/* Responsive Css  */

@media (max-width: 980px) {
    ul{
        flex-direction: column;
    }
    ul li{
        flex-direction: row;
    }
    ul li .progress{
        margin: 0 30px;
    }
    .progress::after{
        width: 5px;
        height: 55px;
        bottom: 30px;
        left: 50%;
        transform: translateX(-50%);
        z-index: -1;
    }
    .one::after{
        height: 0;
    }
    ul li .icon{
        margin: 15px 0;
    }
}

@media (max-width:600px) {
    .head .head_1{
        font-size: 24px;
    }
    .head .head_2{
        font-size: 16px;
    }
}





</style>