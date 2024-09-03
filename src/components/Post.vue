<script setup>
defineProps({
    post: Object
})
const emit = defineEmits(['remove'])

function removePost(id) {
    emit('remove', id)
}
</script>

<template>
    <div class="post">
        <div class="post__content">
            <p>
                <span>id:</span> {{ post.id }}
            </p>
            <p>
                <span>Название поста:</span> {{ post.title }}
            </p>
            <p>
                <span>Содержимое поста:</span> {{ post.body }}
            </p>
        </div>
        <button @click="() => removePost(post.id)">
            X
        </button>
    </div>
</template>

<style scoped>
.post {
    display: flex;
    gap: 20px;
    justify-content: space-between;
    align-items: flex-start;
    padding: 20px;
    border: 2px solid darkmagenta;
}

.post span {
    font-weight: 600;
    color: darkmagenta;
}


.input {
    width: 100%;
    padding: 7px;
}

button {
    padding: 7px 15px;
    background: transparent;
    border: 2px solid darkmagenta;
    color: darkmagenta;
    cursor: pointer;
}

button:hover {
    background: darkmagenta;
    color: white;
}
</style>
