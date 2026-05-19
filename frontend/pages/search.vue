<template>
  <div>
    <h1>Search</h1>

    <input v-model="query" type="text" placeholder="Search by title or author..." />

    <div v-if="filteredPosts.length === 0">
      <p>No posts found.</p>
    </div>

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

const query = ref('')

const filteredPosts = computed(() => {
  if (!query.value) return posts.value
  const q = query.value.toLowerCase()
  return posts.value.filter(p =>
    p.title.toLowerCase().includes(q) ||
    p.author.toLowerCase().includes(q)
  )
})
</script>