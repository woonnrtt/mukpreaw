<template>
<div>
<h1>แก้ไขรายวิชา</h1>
<form v-on:submit.prevent = "editBlog">
    <div class="box">
<p>รหัสวิชา: <input type="text" v-model="blog.title"></p>
<p>ชื่อรายวิชา: <input type="text" v-model="blog.content"></p>
<p>อาจารย์ประจำวิชา: <input type="text" v-model="blog.category"></p></div>
<p>
<button type="submit">update</button>
<button v-on:click="navigateTo('/blogs')">กลับ </button>
</p>
</form>
</div>
</template>
<script>
import BlogsService from '@/services/BlogsService'
export default {
data () {
return {
blog: {
title: '',
thumbnail: 'null',
pictures: 'null',
content: '',
category: '',
status: ''
}
}
},
methods: {
async editBlog () {
try {
await BlogsService.put(this.blog)
this.$router.push({
name: 'blogs'
})
} catch (err) {
console.log(err)
}
}
},
async created () {
try {
let blogId = this.$route.params.blogId
this.blog = (await BlogsService.show(blogId)).data
} catch (error) {
console.log (error)
}
}
}
</script>
<style >
.box{
    background-color: rgb(226, 154, 67);
    margin: 5px;
    padding-left: 10px;
    padding: 10px;
}
</style>