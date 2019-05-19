<template>
<div>
    <h1>Todo List App</h1>
    <input @keyup.enter="addItem" type="text" v-model="inputText" placeholder="gimme some text">
    <div class="addBtn"><button @click="addItem">Add new item</button></div>
    <ul>
        <todo-list-item 
            v-for="(item, index) in items" :key="index"
            v-bind:item="item"
            @remove="removeItem(index)"
            @done="markAsDone(index)" 
            @edit="editItemText"/>
    </ul>
</div>

</template>

<script>
import TodoListItem from './TodoListItem';

    export default {
        components:{
            TodoListItem
        },
        data() {
            return{
                items: [],
                inputText: ''
            }
        },
        created() {
            this.items = JSON.parse(localStorage.getItem('todo-list')) || []
        },
        methods: {
           
            updateStorage(){
                console.log(this.items);
                
                localStorage.setItem('todo-list',JSON.stringify(this.items));
            },
            
            addItem() {
                if(this.inputText === '') return;

                const newItem = {
                    done: false,
                    text: this.inputText
                }
                this.items.push(newItem)
                this.updateStorage()
                this.inputText = '';
            },
            removeItem(index){
                
                this.items.splice(index, 1)
                
                this.updateStorage()
            },
            markAsDone(index){
                this.items[index].done = !this.items[index].done;
                this.updateStorage()
                
            },
            editItemText(index, item){
                this.items[index] = item;
                this.updateStorage()
            }
        }
    }
</script>

<style scoped>
    input{
        border: 1px solid black;
        background: lightgray;
        padding: 5px 10px;
        outline: none;
        width: 500px;
        height: 50px;
        font-size: 2.5em;
    }
    
    input:focus{
        border: 1px solid black;
        background: lightgreen;
        padding: 5px 10px;
        outline: none;
        width: 500px;
        height: 50px;
        font-size: 2.5em;
    }
    
    h1{
        font-size: 3em;
    }

    .addBtn{
        background: white;
        outline: none;
        font-size: 1em;
        margin-left: 50%;
        transform: translateX(-50%);
    }

    button{
        border: 2px solid black;
        background: white;
        outline: none;
        font-size: 1em;
    }

    
    button:active{
        border: 2px solid black;
        background: lightblue;
        outline: none;
        font-size: 1em;
    }

    ul{
        list-style: none;
        padding: 0;
    }
</style>