<template>
  <div>
    <NuxtLink to="/" class="back-link">← Back to Home</NuxtLink>

    <div v-if="post">
      <h1>{{ post.title }}</h1>
      <p class="post-meta">
        By {{ post.author }}
        <span class="badge">{{ post.category }}</span>
      </p>

      <div class="post-content">
        <div v-for="(block, index) in post.content" :key="index">
          <p v-if="block.type === 'paragraph'">
            {{ block.children.map(c => c.text).join('') }}
          </p>
          <h2 v-else-if="block.type === 'heading' && block.level === 2">
            {{ block.children.map(c => c.text).join('') }}
          </h2>
          <h3 v-else-if="block.type === 'heading' && block.level === 3">
            {{ block.children.map(c => c.text).join('') }}
          </h3>
        </div>
      </div>
    </div>

    <div v-else>
      <p>Post not found.</p>
    </div>
  </div>
</template>

<script setup>
const route = useRoute()
const documentId = route.params.documentId

const { data } = await useFetch(`http://localhost:1337/api/a3s/${documentId}`)
const post = computed(() => data.value?.data || null)
</script>