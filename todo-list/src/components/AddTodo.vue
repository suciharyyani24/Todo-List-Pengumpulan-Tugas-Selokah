<template>
<div class="flex space-x-4">
    <input
    v-model="newTodo"
    placeholder="Masukan tugas baru"
    class="flex-grow border border-gray-300 px-4 py-2 rounded-md " />
    <input type="date" v-model="deadline" class="border border-gray-300 px-4 py-2 rounded-md" />
    <button @click="submitTodo" class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600">Tambah</button>
</div>
</template>

<script>
export default {
    data() {
        return {
            newTodo: '',
            deadline:""
        };
    },
    methods: {
        submitTodo() {
            if (this.newTodo.trim() && this.deadline) {
                this.$emit('add-todo', { text:this.newTodo, deadline: this.deadline});
                this.newTodo = '';
                this.deadline = '';
            }
        }
    }
};
</script>