<template>
    <div id="Todo mt-4">
        <ul class="list-group">
            <li class="list-group-item d-flex justify-content-between" v-bind:key="todo.id" v-for="todo in todos">
                <h1>{{todo.title}}</h1>
                <button class="btn btn-outline-danger rounded-circle" @click="$emit('del-todo',todo.id)">x</button>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name:"todo",
    props:['todos'],
}
</script>
