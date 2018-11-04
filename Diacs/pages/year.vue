<template>
  <div id="app">
      <div id="calendar-nav">
          <i class="fas fa-chevron-left" v-on:click="moveLastMonth"></i>
          <span>{{calData.year}}.{{getMonthName(calData.month)}}</span>
          <i class="fas fa-chevron-right"  v-on:click="moveNextMonth"></i>
      </div>
      <table id="calendar" class="table table-bordered">
        <thead>
              <tr>
                  <th v-for="week in weeks">{{week}}</th>
              </tr>
          </thead>
          <tbody>
              <tr v-for="week in calendar">
                  <td v-for="day in week" class="bg" v-bind:style="{backgroundColor:day.color}">
                    <div v-on:click="click(day)">
                      {{day.day}}

                    </div>
                  </td>
              </tr>
          </tbody>
      </table>
      <a href="post"><i class="fas fa-plus"></i></a>

  </div>

</template>

<script>

import Vue from 'vue'

// Font Awesome のメインファイルを import

import '@fortawesome/fontawesome-free-webfonts/css/fontawesome.css'

// 使用するカテゴリーのファイルを import

import '@fortawesome/fontawesome-free-webfonts/css/fa-brands.css'
import '@fortawesome/fontawesome-free-webfonts/css/fa-regular.css'
import '@fortawesome/fontawesome-free-webfonts/css/fa-solid.css'
import axios from 'axios'

export default {
  data: {
    color: [],
    month:[],
    day:[],

  },
  mounted() {
  },
  data: function(){
        return{
          weeks: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
          calData: {year: 0, month: 0},
          items: [],
        }
    },
    created: async function (){
        var date = new Date();
        this.calData.year = date.getFullYear();
        this.calData.month = date.getMonth() + 1;

        this.items = await axios.get("http://ec2-18-191-90-196.us-east-2.compute.amazonaws.com:8080/getCalender/test3")
    },
    methods: {
        click(obj){
            alert(obj.article);
        },
        getMonthName(month){
            var monthName = ['January','February','March','April','May','June','July','August','September','October','November','December'];
            return monthName[month - 1];
        },
        moveLastMonth() {
            if (this.calData.month == 1) {
                this.calData.year--;
                this.calData.month = 12;
            }
            else {
                this.calData.month--;
            }
        },
        moveNextMonth() {
            if (this.calData.month == 12) {
                this.calData.year++;
                this.calData.month = 1;
            }
            else {
                this.calData.month++;
            }
        }
    },
    computed: {
        calendar: function () {
          if (!this.items.data) return;
            console.log(this.items.data[0].Day);
            // 1日の曜日
            var firstDay = new Date(this.calData.year, this.calData.month - 1, 1).getDay();
            // 晦日の日にち
            var lastDate = new Date(this.calData.year, this.calData.month, 0).getDate();
            // 日にちのカウント
            var dayIdx = 1;

            var calendar = [];
            for (var w = 0; w < 6; w++) {
                var week = [];

                // 空白行をなくすため
                if (lastDate < dayIdx) {break;}

                for (var d = 0; d < 17; d++) {
                    if (w == 0 && d < firstDay) {
                        week[d] = {day: ''};
                    } else if (w == 16 && lastDate < dayIdx) {
                        week[d] = {day: ''};
                        dayIdx++;
                    } else if (lastDate < dayIdx) {
                        week[d] = {day: ''};
                        dayIdx++;
                    } else {
                        week[d] = {day: dayIdx};

                        for(var i=0;i<this.items.data.length;i++){
                          if(dayIdx == this.items.data[i].Day){
                            week[d].color = "#"+(this.items.data[i].ColorCode).toString(16)
                            week[d].num = this.items.data.length
                            week[d].article = this.items.data[i].Article
                          }
                        }
                        dayIdx++;
                    }
                }

                calendar.push(week);
            }
            return calendar;
        }
    }
}
</script>

<style>
*{
  margin: 0 auto;
}

.bg{

}


/* カレンダーナビのスタイル */
#calendar-nav {
    text-align: center;
}

#calendar-nav span {
    display: inline-block;
    width: 200px;
}

#calendar-nav i{
  width:10px;
  color:#919191;
}

#calendar-nav i:hover {
    cursor: pointer;
    width:10px;
    color: #919191;
}
#calendar-nav i:visited {
    cursor: pointer;
    width:10px;
    color: #919191;
}

/* カレンダーのスタイル */
span{
  margin-top: 25px;
  color:#919191;
}

.table{
  width:100%;
  /*height:1000px;*/
}
.table th{
    text-align: center;
    width: 23px;
    height: 15px;
    font-size: 13px;
    color:#919191;
    padding-top: 15.7px;
}
.table td{
    text-align: center;
    border: medium solid #F2F2F2;
    width: 51px;
    height: 49px;
    padding: 0;
    margin: 0 auto;
    color:#919191;
}

.tbody{
}

.glyphicon{
  width:10px;
}

#calendar th:first-child {
    color: #C46D6D;
}
/*#calendar {
  background-color: blue;
}*/
#calendar th:nth-child(7) {
    color: #5888B7;
}
#calendar td:nth-child(7) {
    /*background-color: #DFFFFF*/
}

#calendar td:hover {
    opacity: 0.6;
}

#calendar td:visited {
    opacity: 0.6;
    background-color: blue;
}

.fa-plus{
  position: absolute;
  top: 25px;
  right: 15px;
  font-size: 1.5em;
  color: #919191;
}
/*色付け*/


</style>
