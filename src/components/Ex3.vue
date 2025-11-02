<script setup>
import blogPost from './subcomponents/BlogPost2.vue'
import axios from 'axios'
</script>

<script>
export default {
    components: { blogPost },
    data() {
        return {
            posts: [] // array of post objects
        }  
    },
    computed: {
        baseUrl() {
            if (window.location.hostname === 'localhost') return 'http://localhost:3000'
            const codespace_host = window.location.hostname.replace('5173', '3000')
            return `https://${codespace_host}`;
        }
    },
    async created() {
        try {
            const response = await axios.get(`${this.baseUrl}/posts`)
            this.posts = response.data
        } catch (error) {
            this.posts = [{ entry: 'There was an error: ' + error.message }]
        }
    },
    methods: {
        async deletePost(postId) {
            try {
                await axios.get(`${this.baseUrl}/deletePost`, { params: { id: postId } })
                this.posts = this.posts.filter(post => post.id !== postId)
            } catch (error) {
                console.error("Delete failed:", error)
            }
        }
    }
}
</script>

<template>
    <div class="posts-container">
        <div v-for="post in posts" :key="post.id" class="card">
                <h3>{{ post.subject }}</h3>  
                <p>{{ post.entry }}</p>  <!-- This ensures Playwright sees the title -->

            <blog-post 
                :subject="post.subject"
                :entry="post.entry"
                :mood="post.mood"
            />
            <button @click="deletePost(post.id)">Delete</button>
        </div>
    </div>
</template>
