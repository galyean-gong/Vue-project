<template>
  <div id="app">
    <h1 v-text='title'></h1>
    <input type="text" v-model='content' @keyup.enter='enter'>
    <ul>
      <li v-for='item in items' :class="{list:item.islist}" @click='add(item)'>{{item.text}}</li>
    </ul>
    <p>this is child:{{newparams}}</p>
    <compontent-a :msgs='title' @myevent='myfun'></compontent-a>
  </div>
</template>

<script>
import Store from './store.js';
import compontentA from './compontents/compontents.vue'
export default {
  name: 'app',
  data () {
    return {
      title:'To Do List',
      content:'',
      //将取到的值存进去，娶不到为空
      items:Store.fetch(),
      newparams:''
    }
  },
  components:{compontentA},
  methods:{
    add(item){
      item.islist = !item.islist
    },
    enter(){
      this.items.push({
        text:this.content,
          islist:false
      }),
      this.content = ''
    },
    myfun(msg){
      this.newparams = msg
    }

  },
  watch:{ 
      // 监听items变换的值
      items: {
      handler: function (items) { /*存下来 */Store.save(items) },
      // 认为状态可以改变
      deep: true
    }
  }
}
</script>

<style>
.list{
  text-decoration: underline!important;

}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
