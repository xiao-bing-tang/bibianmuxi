<template>
    <div class="todo-header">
        <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="title" @keyup.enter="add"/>
    </div>
</template>

<script>
import {nanoid} from 'nanoid'
export default {
    name:'Title',
    props:['addtodo'],
    data(){
        return{
            title:''
        }
    },
    methods:{
        add(){
            //uuid唯一字符串,nanoid为其简化版
            //校验数据
            if(!this.title.trim()) return alert('请输入内容')
            //将用户输入的内容包装为todo对象
            const todo = {id:nanoid(),title:this.title,done:false}
            //调用App.vue中传过来的函数addtodo添加todo对象
            this.addtodo(todo)
            this.title = ''
        }
    }
}

</script>
<style scoped>
/*header*/
    .todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
    }

    .todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
    }
</style>