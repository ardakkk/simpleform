<template>
  <div id="app">
   <div class="lc-item">
    <div class="lc-item-title">
      График работы
    </div>
    <div class="lc-schedule-days">
      <div class="head requied">Укажите рабочие дни</div>
      <ul>
        <li>
          <input type="checkbox" name="day-1"  value="monday" id="day-1" checked v-model="days">
          <label for="day-1">Пн</label>
        </li>
        <li>
          <input type="checkbox" name="day-2" value="thuesday" id="day-2" checked v-model="days">
          <label for="day-2">Вт</label>
        </li>
        <li>
          <input type="checkbox" name="day-3" value="wednesday" id="day-3" checked v-model="days">
          <label for="day-3">Ср</label>
        </li>
        <li>
          <input type="checkbox" name="day-4" id="day-4" value="thursday" checked v-model="days">
          <label for="day-4">Чт</label>
        </li>
        <li>
          <input type="checkbox" name="day-5" id="day-5" value="friday" checked v-model="days">
          <label for="day-5">Пт</label>
        </li>
        <li>
          <input type="checkbox" name="day-6" id="day-6" value="saturday" v-model="days">
          <label for="day-6">Сб</label>
        </li>
        <li>
          <input type="checkbox" name="day-7" id="day-7" value="sunday" v-model="days">
          <label for="day-7">Вс</label>
        </li>
      </ul>
    </div><!--.schedule-days end-->
    <div class="lc-schedule-time">
      <div class="head requied">Укажите время</div>
      <div style="float:left;">От &nbsp;</div>
      <ul class="time-from">
        <li>
          <select name="time-from-hours" id="time-from-hours" class="lc-select" v-model="schedule.AtHour">
            <option>00</option>
            <option>01</option>
            <option>02</option>
            <option>03</option>
            <option>04</option>
            <option>05</option>
            <option>06</option>
            <option>07</option>
            <option>08</option>
            <option selected>09</option>
            <option>10</option>
            <option>11</option>
            <option>12</option>
            <option>13</option>
            <option>14</option>
            <option>15</option>
            <option>16</option>
            <option>17</option>
            <option>18</option>
            <option>19</option>
            <option>20</option>
            <option>21</option>
            <option>22</option>
            <option>23</option>
          </select> 
        </li>
        <li>
          <select name="time-from-minutes" id="time-from-minutes" class="lc-select" v-model="schedule.AtMinute">
            <option selected>00</option>
            <option>05</option>
            <option>10</option>
            <option>15</option>
            <option>20</option>
            <option>25</option>
            <option>30</option>
            <option>35</option>
            <option>40</option>
            <option>45</option>
            <option>50</option>
            <option>55</option>
          </select> 
        </li>
      </ul>
      <div style="float:left;">до &nbsp;</div>
      <ul class="time-to">
        <li>
          <select name="time-to-hours" id="time-to-hours" class="lc-select" v-model="schedule.BeforeHour">
            <option>00</option>
            <option>01</option>
            <option>02</option>
            <option>03</option>
            <option>04</option>
            <option>05</option>
            <option>06</option>
            <option>07</option>
            <option>08</option>
            <option>09</option>
            <option>10</option>
            <option>11</option>
            <option>12</option>
            <option>13</option>
            <option>14</option>
            <option>15</option>
            <option>16</option>
            <option>17</option>
            <option selected>18</option>
            <option>19</option>
            <option>20</option>
            <option>21</option>
            <option>22</option>
            <option>23</option>
          </select> 
        </li>
        <li>
          <select name="time-to-minutes" id="time-to-minutes" class="lc-select" v-model="schedule.BeforeMinute">
            <option selected>00</option>
            <option>05</option>
            <option>10</option>
            <option>15</option>
            <option>20</option>
            <option>25</option>
            <option>30</option>
            <option>35</option>
            <option>40</option>
            <option>45</option>
            <option>50</option>
            <option>55</option>
          </select> 
        </li>
      </ul>
    </div><!--lc-scheulde-time end-->
    <div class="lc-schedule-options">
      <div class="lc-item-radio">
        <div class="cat-filter-checkbox lc-radio-point">
          <input type="checkbox" name="lc-time-options" id="lc-time-round"/>
          <span class="box"></span><label for="lc-time-round">Круглосуточно</label>
        </div>
        <div class="cat-filter-checkbox lc-radio-point">
          <input type="checkbox" name="lc-time-options" id="lc-time-last"/>
          <span class="box"></span><label for="lc-time-last">До последнего клиента</label>
        </div>
      </div>
    </div><!--.lc-schedule-options end-->
    <div class="lc-item-social-add">
      <a href="#" v-on:click="add">Добавить график</a>
    </div>
  </div><!--.lc-item end-->
  <div class="lc-submit-btns">
    <input type="submit" name="lc-save-info" class="lc-item-save-btn" value="Сохранить">
  </div>
  <div class="lc-result">
    <div class="block">
      <ul>
        <li v-if="block" v-for="item in schedule">Day: {{item.day}} At {{item.AtHour}}-{{item.AtMinute}} to {{item.BeforeHour}}-{{item.BeforeMinute}} <button id="delete" v-on:click="deleteItem(item)">Delete</button></li>
     </ul>
    </div>
  </div>
</div>
</template>

<script>
import Hello from './components/Hello'
import Result from './components/Result'

export default {
  name: 'app',
  components: {
    Hello,'result':Result
  },
  data(){
    return{
      days:[],
      schedule:[
      {day:[],AtHour:"",AtMinute:"",BeforeHour:"",BeforeMinute:""}
      ],
      block: false
    }
  },
  methods:{
    add:function(){
      this.schedule.day = this.days;
      this.block = true;
    },
    deleteItem(item){
      this.schedule.splice(0,1);
    }
  }
}
</script>

<style>
.block {
  position: relative;
  border: 1px solid #eb284f;
  margin-top: 20px;
}
.block ul li {
  margin-bottom: 30px;
  list-style: none;
}
#delete {
  position: absolute;
  right: 20px;
  background-color: #eb284f;
  border: none;
  outline: none;
  color: #fff;
  width: 100px;
  height: 30px;
  cursor:pointer;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.lc-item {
  padding: 32px 0 8px 24px;
  border-top: 1px solid #e1e1e1;
  overflow: hidden;
  margin: 0 24px 0 0;
}
.lc-item-title {
  font-size: 22px;
  font-weight: 600;
  line-height: 1.45;
  color: #585766;
  margin-bottom: 32px;
}
.lc-item .lc-item-title span {
  display: block;
  padding-top: 4px;
  font-size: 15px;
  font-weight: normal;
  font-style: italic;
  line-height: 1.6;
  color: #a2a1b3;
}
.lc-schedule-days {
  width: 100%;
  overflow: hidden;
  height: auto;
  margin-bottom: 32px;
}
.head {
  margin-bottom: 16px;
  font-size: 14px;
  line-height: 1.43;
  letter-spacing: 0.8px;
  font-weight: bold;
  font-style: normal;
  font-stretch: normal;
  color: #585766;
  text-transform: uppercase;
  display: block;
}
.lc-item .head.requied:after {
  content: ' *';
  font-size: 16px;
  font-weight: bold;
  line-height: 1.25;
  letter-spacing: 0.9px;
  color: #eb284f;
}
.lc-schedule-days ul {
  padding: 0;
  margin: 0;
  overflow: hidden;
}
.lc-schedule-days ul li {
  display: block;
  overflow: hidden;
  float: left;
  width: 54px;
  margin-right: 16px;
  background-color: #ffffff;
}
.lc-schedule-days ul li input:checked + label {
  border-color: #eb284f;
  color: #eb284f;
}
.lc-schedule-days ul li label {
  display: block;
  position: relative;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  height: 100%;
  width: 100%;
  -webkit-border-radius: 5px;
  border-radius: 5px;
  border: solid 1px #d9d9d9;
  font-family: Circe;
  font-size: 16px;
  font-weight: bold;
  line-height: 3.4;
  text-align: center;
  color: #74737f;
}
.lc-schedule-days ul li input:checked + label:before {
  position: absolute;
  top: 7px;
  right: 7px;
  content: " ";
  width: 8px;
  height: 7.4px;
  background:  #fff;
}
.lc-schedule-time {
  overflow: hidden;
  width: 100%;
  height: auto;
  margin-bottom: 16px;
}
.lc-schedule-time ul {
  float: left;
  position: relative;
  overflow: hidden;
  padding: 0;
  margin: 0;
}
.lc-schedule-time ul li:first-child {
  padding-right: 13px;
}
.lc-schedule-time ul li {
  float: left;
  overflow: hidden;
  position: relative;
  width: 68px;
  height: 48px;
}
.lc-schedule-options {
  overflow: hidden;
  width: 100%;
  height: auto;
} 
.lc-item .lc-item-radio {
  position: relative;
  float: left;
  width: auto;
  margin-bottom: 32px;
}
.lc-item .lc-item-radio .lc-radio-point {
  float: left;
  width: auto;
  margin-right: 32px;
  font-size: 16px;
  color: #74737f;
}
.cat-filter-checkbox {
  width: 100%;
  height: auto;
  overflow: hidden;
  position: relative;
  font-size: 14px;
  color: #74737f;
  cursor: pointer;
  margin-bottom: 12px;
}
.lc-item .lc-item-social-add {
  float: left;
  position: relative;
  font-size: 16px;
  font-weight: 600;
  line-height: 1.5;
  margin-bottom: 32px;
}
.lc-item .lc-item-social-add a {
  border-color: rgba(235, 40, 79, 0.4);
  margin-left: 31px;
}
.lc-item-save-btn {
  width: 100%;
  height: 56px;
  border: none;
  font-size: 18px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
  background-color: #eb284f;
  -webkit-box-shadow: 0 2px 7px 0 rgba(0, 0, 0, 0.15);
  box-shadow: 0 2px 7px 0 rgba(0, 0, 0, 0.15);
  cursor: pointer;
  padding: 0;
  font-weight: bold;
  line-height: 1.2;
  text-align: center;
  color: #fff;
}

</style>
