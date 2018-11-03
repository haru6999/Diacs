<template>
  <div id="app">
      <div id="calendar-nav">
          <i class="fas fa-chevron-left" v-on:click="moveLastMonth"></i>
          <span>{{calData.year}}.{{getMonthName(calData.month)}}.{{calData.date}}</span>
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
                  <td v-for="day in week">
                    <div class={{}}>
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
  data: function(){
        return{
          weeks: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'],
          calData: {year: 0, month: 0}
        }
    },
    created: function (){
        var date = new Date();
        this.calData.year = date.getFullYear();
        this.calData.month = date.getMonth() + 1;
    },
    methods: {
        getMonthName(month){
            var monthName = ['1','2','3','4','5','6','7','8','9','10','11','12'];
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

                for (var d = 0; d < 7; d++) {
                    if (w == 0 && d < firstDay) {
                        week[d] = {day: ''};
                    } else if (w == 6 && lastDate < dayIdx) {
                        week[d] = {day: ''};
                        dayIdx++;
                    } else if (lastDate < dayIdx) {
                        week[d] = {day: ''};
                        dayIdx++;
                    } else {
                        week[d] = {day: dayIdx};
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
}

/* カレンダーのスタイル */
span{
  margin-top: 15px;
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
    height: 113.74px;
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

/*色付け*/


</style>
