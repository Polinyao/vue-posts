<script setup>
import { ref, onMounted } from 'vue'

import Post from './components/Post.vue'

const posts = ref([])

const newTitle =ref('')
const newBody =ref('')
const countId = ref(20)

onMounted(async() => {
  fetch('https://jsonplaceholder.typicode.com/posts?_limit=20')
      .then(response => response.json())
      .then(json => {
        console.log(json)
        posts.value = json
        console.log(posts.value )
      })
})

function addPost(params) {
  countId.value += 1
  posts.value.push({
    id:countId.value,
    title: newTitle.value,
    body: newBody.value
  })
  newTitle.value = ''
  newBody.value = ''
}

function removePost(id) {
  posts.value = posts.value.filter(post => post.id !== id)
}

</script>

<template>
  <div class="container">
    <div class="controls-posts">
      <input 
        v-model="newTitle" 
        class="input" 
        type="text" 
        placeholder="Название поста"
      >
      <input 
        v-model="newBody" 
        class="input"  
        type="text"
        placeholder="Содержимое поста"
      >
      <button @click="addPost">
        Добавить пост
      </button>
    </div>
    
      <TransitionGroup 
        name="list" 
        tag="div" 
        class="posts"
      >
        <Post
          v-for="post in posts" 
          :key="post.id"
          :post="post"
          @remove="removePost"
        />
      </TransitionGroup>
  </div>
</template>

<style scoped>
.container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 20px;
}

.posts {
  display: flex;
  flex-direction: column;
  gap: 15px;
  margin-top: 20px;
}

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

.controls-posts {
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: flex-end;
  padding: 20px;
  gap: 15px;
  border: 2px solid darkmagenta;
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

.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
