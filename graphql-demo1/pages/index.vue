<template>
  <div class="container">
    <div class="rounded border m-2">
      <h1 class="p-2 text-4xl font-semi-bold text-gray-800">
        Nuxt.js Querying a GraphQL API
      </h1>
      <div class="flex p-2" v-if="!$apollo.queries.streamings.loading">
        <ul class="w-100 px-2 rounded border text-gray-600">
          <li
            v-for="streaming in streamings.items"
            :key="streaming.id"
            class="py-2"
          >
            <a
              v-bind:href="streaming.slug"
              class="w-full inline-block px-6 py-2 text-xs font-medium leading-6 text-center text-black uppercase transition bg-gray-100 rounded shadow ripple hover:shadow-lg hover:bg-gray-200 focus:outline-none"
            >
              {{ streaming.title }}
            </a>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'IndexPage',
  apollo: {
    streamings: gql`
    query streamings {
      streamings (
        order: {scheduleDate: DESC}
      ) {
        items {
          id,
          title,
          slug,
          scheduleDate
        }
      }
    }
    `
  },
  head() {
    return {
      title: 'Le mie dirette!',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'L\'elenco delle mie dirette'
        },
        {
          hid: 'keywords',
          name: 'keywords',
          content: 'asp.net core, blazor, dotnet, azure'
        }
      ]
    }
  }
}
</script>
