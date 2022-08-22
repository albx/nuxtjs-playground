<template>
    <article>
        <h1>{{ article.data.title }}</h1>
        <div>
            {{ article.content }}
        </div>
    </article>
</template>

<script lang="ts">
import Vue from 'vue'
import type { Post } from './post'
import matter from 'gray-matter'

export default Vue.extend({
    async asyncData({ params }): Promise<{ article: any }> {
        const articleFile = await fetch('http://localhost:3000/data/' + params.slug + '.md')
            .then(response => response.text())
        const articleContent = matter(articleFile);

        const article = {
            ...articleContent
        }

        return { article }
    }
})
</script>