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
                    text: this.inputText,
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
            },
            
            // getCurrentTime(){
            //     var today = new Date();
            //     var date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
            //     var time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
            //     return date+' '+time;
            // }
        }
    }
</script>

<style scoped>


    input{
        border: 1px solid #05386b;
        background: #8ee4af;
        border-radius: 15px;
        padding: 5px 10px;
        outline: none;
        width: 470px;
        height: 50px;
        font-size: 2.5em;
        text-align: center;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        
    }
    
    input:focus{
        border: 1px solid #05386b;
        background: #edf5e1;
        border-radius: 20px;
        text-align: center;
        padding: 5px 10px;
        outline: none;
        width: 500px;
        height: 50px;
        font-size: 2.5em;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    }
    
    h1{
        font-size: 5em;
        color: #05386b;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    }

    .addBtn{
        background: #5cdb95;
        outline: none;
        margin-left: 50%;
        transform: translateX(-50%);
        margin-bottom: 50px;
    }

    button{
        margin-top: 5px;
        border: 2px solid #05386b;
        background: #05386b;
        color: #edf5e1;
        border-radius: 10px;
        outline: none;
        font-size: 2em;
        text-align: center;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    }

    button:hover{
        margin-top: 5px;
        border: 2px solid #05386b;
        background:#edf5e1;
        color:#05386b;
        border-radius: 10px;
        outline: none;
        font-size: 2em;
        text-align: center;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    }

    
    button:active{
        border: 2px solid #edf5e1;
        border-radius: 20px;
        background: #379683;
        color: #edf5e1;
        outline: none;
        font-size: 2em;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    }

    ul{
        list-style: none;
        padding: 0;
    }
</style>