<template>
    <li>
        <label>
        <!-- checked属性为选中状态，自定义checked属性使其值为todoObj.done的值，实现选中状态 -->
        <input type="checkbox" :checked='todoObj.done' @change="handleCheck(todoObj.id)"/>
        <!-- <input type="checkbox" v-model="ppp.done"> -->
        <span>{{todoObj.title}}</span>
        </label>
        <button class="btn btn-danger" @click="delet(todoObj.id)">删除</button>
    </li>
</template>

<script>
export default {
    name:'Item',
    props:['todoObj','qufan','deletTodo'],
    data(){
        return{
            // ppp:this.todoObj
        }
    },
    methods:{ 
        handleCheck(id){
            //通知App组件将对应id的done取反
            this.qufan(id)
        },
        delet(id){
            if(confirm('确定删除吗？')){
                this.deletTodo(id)
            }
            
        }
    }
}

</script>
<style scoped>
/*item*/
    li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
    }

    li label {
    float: left;
    cursor: pointer;
    }

    li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
    }

    li button {
    float: right;
    display: none;
    margin-top: 3px;
    }
    li:hover{
        background-color: #ddd;
    }
    li:hover button{
        display: block;
    }
    li:before {
    content: initial;
    }

    li:last-child {
    border-bottom: none;
    }

</style>