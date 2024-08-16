<template>
    <div v-if="visible" :class="notificationClass" class="fixed bottom-4 right-4 p-4 rounded-md shadow-lg text-white">
        {{ message }}
    </div>
</template>

<script>
export default {
    props: {
        message: {
            type: String,
            required: true
        },
        type: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            visible: true
        };
    },
    computed: {
        notificationClass() {
            return this.type === 'success' ? 'bg-green-500' : 'bg-red-500';
        }
    },
    mounted() {
        setTimeout(() => {
            this.visible = false;
        }, 3000); // Notifikasi hilang setelah 3 detik
    }
};
</script>

<style scoped>
/* Styling tambahan jika diperlukan */
</style>
