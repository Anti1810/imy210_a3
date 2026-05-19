<template>
  <div>
    <h1>Blog</h1>

    <select v-model="selectedCategory">
      <option value="">All Categories</option>
      <option v-for="category in categories" :key="category" :value="category">
        {{ category }}
      </option>
    </select>

    <div v-for="post in filteredPosts" :key="post.documentId" class="post-card">
      <NuxtLink :to="`/posts/${post.documentId}`">
        <h2>{{ post.title }}</h2>
      </NuxtLink>
      <p class="post-meta">
        By {{ post.author }}
        <span class="badge">{{ post.category }}</span>
      </p>
      <p class="post-snippet">{{ post.snippet }}</p>
    </div>
  </div>
</template>

<script setup>
const { data } = await useFetch('http://localhost:1337/api/a3s')
const posts = computed(() => data.value?.data || [])

const selectedCategory = ref('')
const categories = computed(() => [...new Set(posts.value.map(p => p.category))])

const filteredPosts = computed(() => {
  if (!selectedCategory.value) return posts.value
  return posts.value.filter(p => p.category === selectedCategory.value)
})
</script>