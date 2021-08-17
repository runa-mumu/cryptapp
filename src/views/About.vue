<template>
 <div class="about">
   <div class="detail">
     <h1 class="detail-title"> {{ cryptlist[0].symbol }}の詳細情報</h1>
     <ul>
       <li>取引所ステータス:{{ status }}</li>
       <li>約定価格:{{ cryptlist[0].price }}</li>
       <li>高値:{{ cryptlist[0].high }}</li>
       <li>安値:{{ cryptlist[0].low }}</li>
       <li>終値:{{ cryptlist[0].close }}</li>
      </ul>
    </div>
    <button @click= "$router.push ({ name: 'Home',params: { CryptoCurrency:CryptoCurrency} })">Homeへ</button>
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
    const item= await axios.get(
      `/public/v1/ticker?symbol=${this.CryptoCurrency}`
      ,

    );
    axios.defaults.withCredentials = true;
    console.log(item.data.data)
    const cryptData =item.data.data;
    this.cryptlist =cryptData;
    this.symbol = item.data.data.symbol;
    this.status = item.data.status;
    this.price = item.data.data[0].dataprice;
    this.high = item.data.data.high;
    this.low = item.data.data[0].low;
    this.close = item.data.data[0].close;
    },
  methods: {
    button(){
      this.$router.push('../views/Home.vue')

    }
  }
};

</script>


<style scoped>
.detail {
  background-color: rgb(243, 214, 242);
}
.detail h1{
  color: black;
  font-size: 20px;
}

</style>

