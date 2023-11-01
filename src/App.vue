<template>
  <div class="container d-flex flex-column">
    <div class="header d-flex flex-row justify-center align-center">POSTS</div>
    <div class="content d-flex flex-column">
      <Loader :is-loading="isLoading" />
      <v-list v-if="!isLoading">
        <v-list-item v-for="post in posts" :key="post.id">
          <h1>{{ post.title }}</h1>
          <p>{{ post.body }}</p>
          <v-divider />
        </v-list-item>
      </v-list>
    </div>
    <div class="footer d-flex flex-row justify-center align-center">
      <v-btn variant="elevated" @click="toggleLoader">
        {{ loaderButton }}
      </v-btn>
    </div>
  </div>
</template>

<script setup>
import {computed, ref} from 'vue';
import Loader from '@/Loader.vue';

const isLoading = ref(false);
const posts = ref([]);
const loaderButton = computed(() => isLoading.value ? 'Hide loader' : 'Show loader')

const toggleLoader = () => {
  isLoading.value = !isLoading.value;
};

const fetchData = async () => {
  try {
    isLoading.value = true;
    const response = await fetch('https://jsonplaceholder.typicode.com/posts?_start=0&_limit=5');
    if (!response.ok) {
      throw new Error(response.status);
    }
    posts.value = await response.json();
  } catch (error) {
    console.error('Error while receiving data', error);
  } finally {
    isLoading.value = false;
  }
};

fetchData();
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.container {
  min-height: 100vh;
}

.content {
  flex: 1;
}

.header {
  height: 60px;
  background: aqua;
  font-size: 40px;
}

.footer {
  height: 60px;
  background: aqua;
}
</style>
