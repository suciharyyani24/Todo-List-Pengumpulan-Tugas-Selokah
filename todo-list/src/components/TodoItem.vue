<template>
    <li class="flex items-center justify-between bg-gray-200 p-4 rounded-md shadow">
        <div class="flex items-center">
            <input type="checkbox" v-model="todo.completed" @change="$emit('toggle-complete')" class="mr-4" />
            <div>
                <p :class="{ 'line-through': todo.completed }">{{ todo.text }}</p>
                <p class="text-sm text-gray-600">Deadline: {{ todo.deadline }}</p>
            </div>
        </div>
        <button @click="$emit('delete-todo')" class="bg-red-500 text-white px-4 py-2 rounded-md">
            Hapus
        </button>
    </li>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        }
    }
};
</script>

<style scoped>
.line-through {
    text-decoration: line-through;
}
</style>
