<template>
  <div>
    <a href="calender">calenderへ飛ぶ</a>

    <ul id="v-for-datas">
      <li v-for="(data, key) in datas">
        {{ key }}: {{ data }}
      </li>
    </ul>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  asyncData ({ params }, callback) {
    axios.get('http://ec2-18-191-90-196.us-east-2.compute.amazonaws.com:8080/lastState')
    .then((res) => {
      callback(null, {
        datas: res.data

      })
    })
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
