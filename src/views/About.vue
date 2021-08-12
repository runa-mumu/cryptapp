<template>
  <div id="about">
    <div class="detail">
      <p>テスト</p>
      <h1 class="detail-title"> {{ data.symbol}}の詳細情報</h1>
        <ul>
          <li>取引所ステータス:{{data.status}}</li>
          <li>約定価格:{{data.price}}</li>
          <li>高値{{data.high}}</li>
          <li>安値{{data.low}}</li>
          <li>終値{{data.close}}</li>
        </ul>
    </div>
    <button>Homeへ</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: ["CryptoCurrency"],
  data() {
    return{
      cryptlist2: [
        { name:"",
        status:"",
        price:"",
        hight:"",
        low:"",
        close:""

        },
      ]

    }; 
  },
  async created(){
    const item2= await axios.get(
      `public/public/v1/ticker?symbol=${this.CryptoCurrency2}`
      ,

    );
    axios.defaults.withCredentials = true;
    console.log(item2.data.data)
    const cryptData2 =item2.data.data;
    this.cryptlist2 =cryptData2;
    this.name = item2.data.data[0].symbol;
    this.status = item2.data.data[0].status;
    this.price = item2.data.data[0].price;
    this.high = item2.data.data[0].high;
    this.low = item2.data.data[0].low;
    this.close = item2.data.data[0].close;
    },
  methods: {
    button(){
      this.$router.push('../views/Home.vue')

    }
  }
};

</script>


<style scoped>
.detail{
  background-color: rgb(243, 214, 242);
}
.detail h1{
  color: black;
  font-size: 20px;
}




</style>

