<template>
    <div class="container">
        <div class="nv-navbar">
            <ul class="nav">
                <li><router-link :to="{name: 'blogs'}" >จัดการรายวิชา</router-link></li>
                <li><router-link :to="{name: 'users'}" >จัดการผู้ใช้</router-link></li>
                <li><router-link :to="{name: 'login'}" >Login</router-link></li>
                <li><a v-on:click.prevent="logout" href="#">Logout</a></li>
            </ul>
            <div class="clearfix"></div>
        </div>
    </div>
</template>
<script>
export default {
    methods: {
        logout () {
            this.$store.dispatch('setToken', null)
            this.$store.dispatch('setUser', null)
            this.$router.push({
                name: 'login'
             })
        }
    }
}
</script>
<style scoped>
.nv-navbar {
background-color:rgb(255, 160, 17);
width: 100%;
padding:10px 0px 10px 0px;
text-align: center;
}
.nv-navbar .nav {
list-style: none;
margin:0;
padding:0;
float:left;
}
.nv-navbar .nav li {
float:left;
}
.nv-navbar .nav li a {
padding: 10px;
text-decoration: none;
color:rgb(255, 255, 255);
font-weight: bold;
}
.nv-navbar .nav li a:hover {
padding: 10px;
text-decoration: none;
color:rgb(185, 91, 4);
}
.nv-navbar .nav li a.router-link-active {
background-color:rgb(190, 108, 60);
color:rgb(255, 255, 255);
}
.clearfix {
clear: left;
}
</style>