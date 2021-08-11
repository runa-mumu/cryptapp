<template>
  <div class="about">
    <div class="detail">
      <h1 class="detail-title"> {{data.symbol}}の詳細情報</h1>
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
      cryptlist: [
        { symbol:"",
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
    const item = await axios.get(
      'https://api.coin.z.com/public/v1/ticker'

    );
    console.log(item.data)
    const cryptData =item.data;
    this.cryptlist =cryptData;
  },
  methods: {
    button(){
      this.$router.push('../views/Home.vue')

    }
  }
};

</script>


<style scoped>
.about{
  background-color: rgb(243, 214, 242);
}
.detail {
  color: black;
  font-size: 20px;
}




</style>

