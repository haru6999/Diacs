<template>
  <div>
    <a href="calender">calenderへ飛ぶ</a>
    {{ username }}
    <div class="color">
      background-color:{{color}};
      $color={{color}};
    </div>
    <script>
      var changeColor = function(){
        // search-result-num のクラス名を持つ要素を取得
        var resultNum = document.querySelector('.color');

        // 色変更
        resultNum.style.backgroundColor = '{{color}}';
      }
      // 実行
      changeColor();
    </script>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData(){
    let { data } = await axios.get('http://ec2-18-191-90-196.us-east-2.compute.amazonaws.com:8080/lastState')
    return {username : data.UserName,
      color : "#"+(data.ColorCode).toString(16)
    }
  }
}


</script>

<style>



.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.color{
  width: 100%;
  height: 100vh;
}

</style>
