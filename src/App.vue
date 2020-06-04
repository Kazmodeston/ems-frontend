<template>
  <div>
   <app-header></app-header>
   <app-body></app-body>
  </div>
</template>

<script>
import Header from "./components/Header"
import Body from "./components/Body"

export default {
  components:{
    "app-header":Header,
    "app-body":Body
  },
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style>
h1{
  color: blueviolet;
}
nav{
    background-color: #222;
    padding: 10px 5px;
    margin: 0;
    overflow: hidden;
}
nav > ul{
    padding: 0;
    margin: 0;
    list-style: none;
}
nav > ul > li{
    line-height: 40px;
    float: left;
    margin: 0 25px;
}
nav > ul > li > a{
    color: cornsilk;
    text-decoration: none;
}
nav > ul > li > a:hover{
    color:darkkhaki;
    text-decoration: underline;
}
</style>
