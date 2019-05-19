<template>
    <li class="todo-item">
        <div class="row">
            <button class="saveBtn" v-if="isEditting" @click="callSave">Save</button>
            <button class="editBtn" v-else @click="callEdit">Edit</button>
            <input class v-if="isEditting" type="text" v-model="item.text">
            <div class="todoText" v-if="!isEditting" @click="callDone" :class="{done: item.done}">{{ item.text }}</div>
            <button class="removeBtn" @click="callRemove">X</button>
        </div>
    </li>
</template>

<script>
    export default {
       props:['item'],
       data() { 
            return {
               isEditting:false
            }
       },
       methods:{
           callRemove(){
               this.isEditting = false;
               this.$emit('remove');
           },
           callDone(){
               this.$emit('done');
           },
           callEdit(){
               this.isEditting = true;
           },
           callSave(){
               this.isEditting = false;
               this.$emit('edit', this.item);
           }
           
       }
    }
</script>

<style scoped>
input{
    border: 1px solid black;
    width: 100px;
    margin: 0;
    font-size: 1em;
    text-align: center;
    background-color: orange;
}

.todoText{
    width: 100px;
    margin: 0;
}
.done{
    text-decoration: line-through;
    color: green;
    background-color: lightblue;
    }
    li{
        font-size: 2em
    }

.saveBtn{
    border: 1px solid green;
    font-size: 0.7em;
    padding: 0;
}

.removeBtn{
    border: 1px solid red;
    border-radius: 10px;
    font-size: 0.7em;
    margin-top:0%;
    background-color: red;
    height: 30;
    padding: 0;
}

.editBtn{
    border: 1px solid orange;
    font-size: 0.7em;
    
    padding: 0;
}

.row{
    display: flex;
    justify-content: space-between;
    width: 500px;
    height: 40px;
    margin-left: 50%;
    transform: translateX(-50%);
}

</style>