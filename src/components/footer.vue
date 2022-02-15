<template>
  <!-- v-show="total"，total为0即没有todo时隐藏footer -->
    <div class="todo-footer" v-show="total">
        <label>
          <input type="checkbox" :checked='all' @change="checkAll"/>
        </label>
        <span>
          <span>已完成{{finesh}}</span> / 全部{{total}}
        </span>
        <button class="btn btn-danger" @click="clearAll()">清除已完成任务</button>
  </div>
</template>

<script>
export default {
    name: 'Footer', 
    props:['todos','checkAllTodo','clearAllTodo'],
    computed:{
      total(){
        return this.todos.length
      },
      finesh(){
        // 使用reduce函数累加符合条件的内容，pre初始值为0
        return this.todos.reduce((pre,todo)=>{
          //todo.done的值是否为真，如果为真则使pre加一
          return pre + (todo.done ? 1 : 0)
        },0)
      },
      all(){
        return this.total == this.finesh && this.total>0
      }
    },
    methods:{
      checkAll(e){
        // console.log(e.target.checked);
        this.checkAllTodo(e.target.checked)
      },
      clearAll(){
        this.clearAllTodo()
      }
    }
}

</script>
<style scoped>

/*footer*/
    .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
    }

    .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
    }

    .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
    }

    .todo-footer button {
    float: right;
    margin-top: 5px;
    }

</style>