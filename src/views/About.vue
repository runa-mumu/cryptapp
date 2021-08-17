<template>
 <div class="about">
   <div class="detail">
     <h1 class="detail-title"> {{ cryptlist.symbol }}の詳細情報</h1>
     <ul>
       <li>取引所ステータス:{{ status }}</li>
       <li>約定価格:{{ price }}</li>
       <li>高値:{{ high }}</li>
       <li>安値:{{ low }}</li>
       <li>終値:{{ close }}</li>
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
        { symbol:"テスト",
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
    this.name = item.data.data.symbol;
    this.status = item.data.data.status;
    this.price = item.data.data.price;
    this.high = item.data.data.high;
    this.low = item.data.data.low;
    this.close = item.data.data.close;
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

