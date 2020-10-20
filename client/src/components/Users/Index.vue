<template>
<body>
 <div>
<h2>ผู้เข้าใช้งาน</h2>
<h4>จํานวนผู้ใช้งาน {{users.length}}</h4>
<p><button v-on:click="navigateTo('/user/create')">สร้างผู้ใช้งาน</button></p>
<div class="box1" v-for="user in users" v-bind:key="user.id">
 <p>id: {{ user.id }}</p>
 <p>ชื่อ-นามสกุล: {{ user.name }} - {{ user.lastname }}</p>
 <p>email: {{ user.email }}</p>
 <p>password: {{ user.password }}</p>
 
<button v-on:click="navigateTo('/user/edit/'+ user.id)">แก้ไขข้อมูล
</button>
<button v-on:click="deleteUser(user)">ลบข้อมูล</button>
<p>
 <hr>
</div>
</div></body>
</template>
<script>
import UsersService from '@/services/UsersService'

 export default {
 data () {
 return {
 users: []
 }
 },
 

async created () {
 try {
    this.users = (await UsersService.index()).data
 } catch (error) {
console.log (error)
 }
},

methods: {
 navigateTo (route) {
 this.$router.push(route)
 },

 

 async deleteUser (user) {
 
 await UsersService.delete(user)
 this.refreshData()

 },
 async refreshData() {
 this.users = (await UsersService.index()).data
 }
}
 }
</script>
<style>
   body {
  background-color: rgb(255, 222, 151);
   }
   .box1{
      background-color: white;
      margin: 5px;
      padding: 5px;
   }
   p{
      color: tomato;
   }
</style>