<template>
    <li class="todo-item">
        <div class="row">
            <button class="saveBtn" v-if="isEditting" @click="callSave">-Save-</button>
            <button class="editBtn" v-else @click="callEdit">-Edit-</button>
            <input class @keyup.enter="callSave" v-if="isEditting" type="text" v-model="item.text">
            <div class="todoText" v-if="!isEditting" @click="callDone" :class="{done: item.done}">{{ item.text }}</div>
            <button class="removeBtn" @click="callRemove">-X-</button>
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
    border: 1px solid #05386b;
        background: #8ee4af;
        border-radius: 15px;
        padding: 5px 10px;
        outline: none;
        font-size: 0.6em;
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
        font-size: 0.7em;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    }

.todoText{
    margin: 0;
    text-align: center;
    border: 1px solid #05386b;
    border-radius: 10px;
    background-color: #8ee4af;
     font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;

}

.todoText:hover{
    margin: 0;
    text-align: center;
    border: 1px solid #05386b;
    border-radius: 10px;
    background-color:#edf5e1;
     font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;

}

.done{
    text-decoration: line-through;
    color: #edf5e1;
    background-color: #379683;
    border-radius: 20px;
    }

.done:hover{
    text-decoration: line-through;
    color:#05386b;
    background-color: #edf5e1;
    border-radius: 20px;
    }

    li{
        font-size: 2em
    }

.saveBtn{
    border: 1px solid #edf5e1;
    background-color:#05386b;
    color:#edf5e1;
    font-size: 0.6em;
    border-radius:20px;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    padding: 0;
}

.saveBtn:hover{
    border: 1px solid #05386b;
    background-color:#379683;
    color:#edf5e1;
    font-size: 0.6em;
    border-radius:20px;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    padding: 0;
}

.removeBtn:hover{
    border: 1px solid #05386b;
    border-radius: 100px;
    font-size: 0.3em;
    margin-top:0%;
    background-color: rgb(196, 30, 107);
    color: #05386b;
    font-size: 1em;
    padding: 0;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

.removeBtn{
    border: 1px solid #05386b;
    border-radius: 100px;
    font-size: 0.3em;
    margin-top:0%;
    background-color:#05386b;
    color:  rgb(196, 30, 107);
    font-size: 1em;
    padding: 0;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

.editBtn{
    border: 1px solid #05386b;
    background-color: #edf5e1;
    color: #05386b;
    font-size: 0.7em;
    border-radius:20px;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    padding: 0;
}

.editBtn:hover{
    border: 1px solid #05386b;
    background-color:#379683;
    color: #edf5e1;
    font-size: 0.7em;
    border-radius:20px;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    padding: 0;
}

.row{
    display: flex;
    justify-content: space-between;
    width: 400px;
    height: 40px;
    margin-left: 50%;
    transform: translateX(-50%);
    margin-top: 10px;
}


</style>