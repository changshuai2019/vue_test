<template>
    <div>
        <ul>
            <li v-for="(item,index) in userList" :key="index" @click="clickUser(item.userName,$event)">
                {{item.userName}}---{{userObj.age}}
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: "userlistcom",
        props: {
            userList: Array  ,
            userObj:Object
        },
        methods:{
            clickUser:function (userName,$event) {
                this.$parent.msg=userName;
                console.log($event);
                console.log(this.$emit);
            }
            ,
        }
    }
</script>

<style scoped>

</style>