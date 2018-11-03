<template>
  <a href="calender">calenderへ飛ぶ</a>
</template>

<script>
import axios from 'axios'

export default {
  created:async function () { //読み込まれた時 asyncの下でしかawaitは使えないよ
    let { data } = await axios.get('http://ec2-18-191-90-196.us-east-2.compute.amazonaws.com:8080/getSentiment', {
    });
    console.log(data),
    console.log(data.UserName),
    console.log(data.Article),
    console.log(data.Emotion),
    console.log(data.EmotionNum),
    console.log(data.ColorCode)
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
</style>
