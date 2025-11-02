<script>
import blogPost from './subcomponents/BlogPost.vue'
import axios from 'axios'

export default {
  components: { blogPost },
  data() {
    return {
      posts: [] // array of post objects
    }
  },
  computed: {
    baseUrl() {
      if (window.location.hostname === 'localhost')
        return 'http://localhost:3000'
      else {
        const codespace_host = window.location.hostname.replace('5173', '3000')
        return `https://${codespace_host}`
      }
    }
  },
  async mounted() {
    try {
      // Fetch posts before component mounts
      const response = await axios.get(`${this.baseUrl}/posts`)
      this.posts = response.data
    } catch (error) {
      this.posts = [{ subject: 'Error', entry: 'There was an error: ' + error.message }]
    }
  }
}
</script>

<template>
  <div class="posts-container">
    <div
      v-for="(post, index) in posts"
      :key="index"
      class="card"
    >
    <h3>{{ post.subject }}</h3>
    <p>{{ post.entry }}</p>
      <blog-post
        :subject="post.subject"
        :entry="post.entry"
        :date="post.date"
      />
    </div>
  </div>
</template>