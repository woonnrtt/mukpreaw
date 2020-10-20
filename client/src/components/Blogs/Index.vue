<template>
<div>
<h2>ระบบจัดการวิชาเรียนในคณะ</h2>

<h4>จำนวนวิชา {{blogs.length}}</h4>
<p><button v-on:click="navigateTo('/blog/create')">เพิ่มรายวิชา</button></p>
<div class="box" v-for="blog in blogs" v-bind:key="blog.id">
<p>id: {{ blog.id }}</p>
<p>รหัสรายวิชา: {{ blog.title }}</p>
<p>ชื่อรายวิชา: {{ blog.content }}</p>
<p>อาจารย์ประจำรายวิชา: {{ blog.category }}</p>
<p>
<button v-on:click="navigateTo('/blog/edit/'+ blog.id)">แก้ไขรายวิชา</button>
<button v-on:click="deleteBlog(blog)">ลบข้อมูลรายวิชา</button>
</p>
<hr>
</div>
</div>
</template>
<script>
import BlogsService from '@/services/BlogsService'
export default {
data () {
return {
blogs: []
}
},
async created () {
this.blogs = (await BlogsService.index()).data
},
methods: {

navigateTo (route) {
this.$router.push(route)
},
async deleteBlog (blog) {
let result = confirm("Want to delete?")
if (result) {
try {
await BlogsService.delete(blog)
this.refreshData()
} catch (err) {
console.log(err)
}
}
},
async refreshData() {
this.blogs = (await BlogsService.index()).data
}
}
}
</script>
<style>
 p{
     color :white;
}
.box{
    background-color: rgb(226, 154, 67);
    margin: 5px;
    padding-left: 10px;
    padding: 10px;
}
</style>