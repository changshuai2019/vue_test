<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld :msg='msg' />
    <user-list-com :user-list="userlist" :userObj="userObj"></user-list-com>
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
          userObj:{
              age:18,
              sex:1
          }
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
