<template class="submited__container">
  <div class="submited__container--popup">
    <h1>送信できたよ！</h1>
    <h2>今回の日記カラーは</h2>
    <div class="circle"></div>
    <a href="calender" class="submited__btn--back">カレンダーへ戻る</a>
    <script>
      var changeColor = function(){
        // search-result-num のクラス名を持つ要素を取得
        var resultNum = document.querySelector('.circle');

        // 色変
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

.submited__container {
  /*背景の画像とかよしなに入れて欲しい！*/
  /*background-image: url();*/
  display: flex;
  justify-content: center;
  align-items: center;
}

.submited__container--popup {
  color: #333;
  width: 90%;
  margin: 3rem auto;
  padding: 2rem 0;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  background-color: #fefefe;
  border-radius: 1.5rem;
  box-shadow: 0rem 0rem 0.5rem #aaa;
}

.submited__container--popup h1 {
  font-weight: normal;
}

.submited__container--popup h2 {
  font-weight: normal;
}

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

.circle{
  width: 80px;
  height: 80px;
  border-radius: 50%;
  box-shadow: 0rem 0rem 0.5rem #aaa;
  margin: 1.5rem 0;
}

.submited__btn--back {
  font-size: 1.25rem;
  color: #333;
  text-decoration: none;
}

.submited__btn--back:hover {
  background-color: #707070;
}

</style>
