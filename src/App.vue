<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld :msg='msg' />
    <user-list-com :user-list="userlist" :userObj="userObj"></user-list-com>
    <!--<route-link/>-->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import UserListCom from './components/userlistcom.vue'
export default {
  name: 'App',
  components: {
    HelloWorld,UserListCom
  },
  data:function () {
      return {
          msg:"我的第一个vue项目",
          userlist:[
              {
                  userName:"小明"
              },
              {
                  userName:"小红"
              },
              {
                  userName:"小黑"
              }
          ],
          testTime:[{data:20,time:"2019-07-30 01:01"},{data:20,time:"2020-07-30 00:00"}, {data:229,time:"2019-07-29 00:00"}, {data:220,time:"2019-07-30 01:00"}, {data:1,time:"2019-08-30 00:01"}],
          userObj:{
              age:18,
              sex:1
          }
      }
   },
    created:function(){

    },
    beforeMount:function(){
      var json = {'action':'AGGRE_SDR','columns':[{'id':86400,'style':'IDENTIFIER','type':'TIME'},{'id':'60975910995','style':'NAME','type':'DIMENSION'},{'id':'IOT_ANALYSIS_GRP_IOT_UI_MODEL_TRAFFIC','style':'IDENTIFIER','type':'MODEL'}],'conditions':{'childs':[{'id':86400,'operator':'GE','style':'IDENTIFIER','type':'TIME','values':['1564502400']},{'id':86400,'operator':'LT','style':'IDENTIFIER','type':'TIME','values':['1564588800']},{'id':60975561768,'operator':'IS NOT NULL','style':'IDENTIFIER','type':'TIME','values':['1']}],'relation':'AND'},'limit':5000,'locale':'zh_CH','start':0,'cubes':"aaaaaaaaaaaaaaaa"};
      var newJson = {};
      //先根据type==time找到时间 判断时间大小 修改时间格式
      var startTime = json.conditions.childs[0].values[0];
      var endTime = json.conditions.childs[1].values[0];
      newJson.timeRange=startTime+","+endTime;
      //查询的列
      newJson.columns={};
      //根据id  （86400）获取1day类似
      newJson.columns.interval=json.columns[0].id;
      //如果有维度
      newJson.columns.dimension=json.columns[1].id;
      //如果有指标
      newJson.columns.dimension=json.columns[1].id;
      // 查询的条件
      newJson.conditions=[];
      newJson.conditions.push({
          "dimension": json.conditions.childs[2].id,
          "operator": json.conditions.childs[2].operator, //维度根据in is not null ；指标> < >= <=
          "value": json.conditions.childs[2].values
      });
      newJson.limit = json.limit;
      newJson.locale = json.locale;
      var tempparam = {};
      tempparam.parms = newJson;
      // 匹配出servicecode
      tempparam.servicecode = json.cubes;
      console.log(tempparam);
    },
    mounted:function(){
        var table1=[
            {lineid:1,rate:6,sessions:2,ratio:3},
            {lineid:5,rate:8,sessions:1,ratio:5},
            {lineid:9,rate:4,sessions:2,ratio:2},
            {lineid:2,rate:1,sessions:3,ratio:3},
            {lineid:"99",rate:2,sessions:5,ratio:1},
            // {lineid:"a",rate:4,sessions:3,ratio:9},
            // {lineid:7,rate:5,sessions:7,ratio:3},
        ];
        var table2=[
            {lineid:9,rate_2:4,sessions_2:2,ratio_2:2},
            {lineid:2,rate_2:1,sessions_2:3,ratio_2:3},
            {lineid:"99",rate_2:2,sessions_2:5,ratio_2:1},
            {lineid:"a",rate_2:4,sessions_2:3,ratio_2:9},
            {lineid:1,rate_2:61,sessions_2:2,ratio_2:3,test1:100},
            {lineid:5,rate_2:8,sessions_2:1,ratio_2:5},
            {lineid:7,rate_2:5,sessions_2:7,ratio_2:3}
        ];
        //根据lineid把table2合并到table1//
        var aaa = this.objHeBing(table1,table2,"lineid");
        console.log(aaa);
    },
    methods:{
      objHeBing:function(obj1,obj2,interval){
          if(obj1.length<=obj2.length){
              var temp = obj1;
              obj1 = obj2;
              obj2 = temp;
          }
          obj2.forEach(function(o){
              for(var k in o){
                  obj1.forEach(function(t){
                      for(var key in t){
                          console.log(key);
                          if(t[interval] == o[interval]){
                              t[k] = o[k];
                          }
                      }
                  })
              }
          });
          return obj1;
      },
        testTm:function () {
            var compare = function (val1,val2) {
                return val1.time<val2.time?-1:1;
            };
            console.log(this.testTime.sort(compare))
        }
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
