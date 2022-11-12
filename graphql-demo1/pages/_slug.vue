<template>
  <div class="container">
    <h1>{{streamingBySlug.title}}</h1>

    <p>
      <a href="/">Back</a>
    </p>

    <div>
      <a v-bind:href="streamingBySlug.youTubeVideoUrl" target="_blank">YouTube</a>
    </div>
  </div>
</template>
<script>
import gql from 'graphql-tag'

export default {
  name: 'StreamingDetailPage',
  apollo: {
    streamingBySlug: {
      query: gql`
      query getStreamingDetail ($slug: String!) {
        streamingBySlug(slug: $slug) {
          title,
          slug,
          scheduleDate,
          startingTime,
          endingTime,
          hostingChannelUrl,
          youTubeVideoUrl,
          seo {
            title,
            description,
            keywords
          }
        }
      }
      `,
      variables() {
        return {
          slug: this.$route.params.slug || ''
        }
      }
    }
  },
  head() {
    return {
      title: this.streamingBySlug.seo.title,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.streamingBySlug.seo.description
        },
        {
          hid: 'keywords',
          name: 'keywords',
          content: this.streamingBySlug.seo.keywords
        }
      ]
    }
  }
}
</script>