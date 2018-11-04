<template>
  <div class="main">
    <div id="example-2">
      <input v-model="message" placeholder="今日どんなことがあったの？">
      <button v-on:click="greet">投稿する</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {

  data: function () {
   return
 },
  methods: { //ボタンが押された時
    async greet(event) {
      let params = new URLSearchParams();
      params.append('article', this.message);
      params.append('username', 'taka');
      params.append('year', '2018');
      params.append('month', '12');
      params.append('day', '31');

      let { data } = await axios.post('http://ec2-18-191-90-196.us-east-2.compute.amazonaws.com:8080/getSentiment',params);
      console.log(data)
      console.log(this)
      this.$router.push("completion")
      console.log(this.message)
      console.log(data.UserName)
    }
  }
}
</script>

<style>
.main{
  position: absolute;
  top:250px;
  width: 100%;
}

h2{
  width: 100%;
  text-align: center;
}

input{
  width: 60%;
  height: 50px;
  margin-left: 20%;
  margin-top: 50px;
  box-sizing:border-box;
  border-color: black;
}

button{
  width: 100%;
  margin-top: 50px;
  text-align: center;
}
</style>
