<template>
    <ul class="todo-main">
        <!-- 遍历todos数组使用todoObj存储单项，使用props实现组件通信将todoObj传递给Item组件 -->
        <item v-for="todoObj in todos" :key="todoObj.id" :todoObj='todoObj' :qufan='qufan' :deletTodo='deletTodo'/>
    </ul>
</template>

<script>
import Item from './item.vue'
export default {
    name:'List',
    components:{
        Item
    },
    props:['todos','qufan','deletTodo']
    
}

</script>
<style scoped>
/*main*/
    .todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
    }

    .todo-empty {
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
    }
</style>