<template>
    <selection>
        <transition-group name="list" tag="ul">
            <li v-for="(todoItem,index) in propsData" class="shadow" v-bind:key="todoItem">
                <i class="checkBtn fas fa-check" aria-hidden="true"/>
                {{todoItem}}
                <input type="text" class="fix" placeholder="fixed" />
                <span class="fixBtn" type="button" @click="fixTodo(todoItem,index)">
                <i class="fas fa-wrench" aria-hidden="true"></i>
                </span>
                <span class="removeBtn" type="button" @click="removeTodo(todoItem,index)">
                <i class="far fa-trash-alt" aria-hidden="true"/>
                </span>
            </li>
        </transition-group>
    </selection>
</template>

<script>
export default {
    props:['propsData'],
    methods: {
        removeTodo(todoItem,index) {
            this.$emit('removeTodo',todoItem,index);
        },
        fixTodo(todoItem,index){
            const fixed = document.getElementsByClassName("fix").item(index).value;
            if( fixed !== ""){
            const value = this.todoItem && this.todoItem.trim();
            this.$emit('fixTodo',todoItem,index);
            }
            this.fixed = '';
        }
    }
}
</script>

<style>
    .list-enter-active, .list-leave-active {
        transition: all 1s;
    }
    .list-enter, .list-leave-to{
        opacity: 0;
        transform: translateY(30px);
    }
    ul{
        list-style-type: none;
        padding-left: 0px;
        margin-top: 0px;
        text-align: left; 
    }
    li {
        display: flex;
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin : 0.5rem 0;
        padding : 0 0.9rem;
        background : white;
        border-radius: 5px;
        
    }
    .checkBtn {
        line-height: 45px;
        color : #62ACDE;
        margin-right: 5px;
    }
    .removeBtn {
        margin-left: 20px;
        color:#DE4343;
    }
    .fixBtn {
        margin-left: 20px;
        color:#62ACDE;
    }
    .fix {
        margin-left : auto;
        margin-top : 5px;
        height: 35px;
    }
</style>