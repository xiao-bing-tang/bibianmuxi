<template>
  <div>
    <div class="todo-container">
      <div class="todo-wrap">
        <Title :addtodo='addtodo'/>
        <List :todos='todos' :qufan='qufan' :deletTodo='deletTodo'/>
        <Footer :todos='todos' :checkAllTodo='checkAllTodo' :clearAllTodo='clearAllTodo'/>
      </div>
    </div>
  </div>
</template>

<script>

import Footer from './components/footer.vue'
import List from './components/list.vue'
import Title from './components/title.vue'
export default {
  name: 'App',
  components: {
    Footer,
    List,
    Title
  },
  data(){
    return{
      todos:JSON.parse(localStorage.getItem('todos')) || []
    }
  },
  watch:{
    todos:{
      deep:true, //深度监视,负责无法监视到对象内部变化
      handler(value){
        localStorage.setItem('todos',JSON.stringify(value))
      }
    }
  },
  methods:{
    //将addtodo函数传递给title，在title中调用addtodo函数，从而达到子向父传递
    addtodo(x){
      //使用unshift函数将获取到的todo对象添加到todos内
      this.todos.unshift(x)
      console.log(x);
      localStorage.setItem('todos',JSON.stringify(this.todos))
    },
    qufan(id){
      this.todos.forEach((todo)=>{
        if(todo.id == id){
          //修改todos数据
          todo.done = !todo.done
        }
      })
    },
    //删除todo
    deletTodo(id){
      //使用filter过滤掉符合条件的todo，后将过滤后剩余的内容重新传递给this.todos
      this.todos = this.todos.filter((todo)=>{
        return todo.id !== id
      })
    },
    checkAllTodo(x){
      this.todos.forEach((todo)=>{
        //e.target.checked
        todo.done = x
      })
    },
    //清除选中的
    clearAllTodo(){
      this.todos = this.todos.filter((todo)=>{
        return todo.done !== true
      })
    }
  }
  
}
</script>

<style>
/*base*/
  body {
    background: #fff;
  }

  .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }

  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }

  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }

  .btn:focus {
    outline: none;
  }

  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
