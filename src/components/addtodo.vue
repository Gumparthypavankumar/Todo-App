<template>
    <div class="container my-4">
       <form @submit="addnewTodo">
           <div class="d-flex form-group">
               <input type="text" v-model="title" class="form-control" placeholder="enter title" required/>
           </div>
           <button class="btn btn-primary" type="submit">Add Todo</button>
       </form>
    </div>
</template>

<script>
export default {
    name:"addtodo",
    data(){
        return{
            title:''
        }
    },
    methods:{
        addnewTodo(e)
        {
            e.preventDefault();
            const newTodo={
                title:this.title,
                completed:false
            }
            this.title='';
            this.$emit('add-todo',newTodo)
        }
    }
}
</script>