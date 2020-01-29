<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keyup.enter="addTodo">
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn far fa-plus-square fa-2x" aria-hidden="true"></i>
        </span>
    </div>
</template>

<script>
export default {
    data(){
        return {
            newTodoItem : ''
        }
    },
    methods:{
        addTodo(){
            if(this.newTodoItem !== ""){
                const value = this.newTodoItem && this.newTodoItem.trim();
                this.$emit('addTodo',value);
                localStorage.setItem(this.newTodoItem,this.newTodoItem);
                // key와 value로 이루어짐
                //trim 함수는 공백 없이 처리해줌
                this.clearInput();
            } else {
                alert("공간을 채워주세요!");
            }
        },
        clearInput() {
            this.newTodoItem = '';
        }
    }
}
</script>

<style>
    input:focus{
        outline : none;
    }
    .inputBox{
        background: white;
        height: 50px;
        line-height: 50px;
        border-radius: 5px;
    }
    .inputBox input{
        border-style: none;
        font-size:0.9rem;
    }
    .addContainer{
        float : right;
        background: linear-gradient(to right, #6478FB, #8763FB);
        display: block;
        width: 3rem;
        border-radius: 0 5px 5px 0;
    }
    .addBtn {
        color : white;
        vertical-align: middle;

    }
</style>