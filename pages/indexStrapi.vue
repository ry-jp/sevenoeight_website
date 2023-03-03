<template>
  <div class="h-full w-screen min-h-screen overflow-hidden">
    <!-- <p>
      {{ data }}
    </p> -->
    <div 
      class="w-full h-full flex flex-row space-x-12"
      v-for="{ Title, Content, Image } in data.articles.data.attributes"
      :key="data.articles.data.id"
    >
      <div class="flex flex-col items-start space-y-4 w-1/2">
        <h1 class="text-xl font-semibold">
          {{ Title }}
        </h1>
        <p class="text-base">
          {{ Content }}
        </p>
      </div>
      <div class="w-1/2">
        <nuxt-img :src="'http://localhost:1337'+Image.data.attributes.url" class="object-cover" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">

type Articles = {
  articles: {
    data: {
      id: number,
      attributes: {
        Title: string,
        Content: string,
        Image: {
          data: {
            attributes: {
              url: String
            }
          }
        }
      }
    }[]
  }
}

const query = gql`
  query allArticles {
    articles {
      data {
        id
        attributes {
          Title
          Content
          Image {
            data {
              attributes {
                url
              }
            }
          }
        }
      }
    }
  }
`


const { data, error, refresh } : any = await useAsyncQuery<Articles>(query)




</script>

<style scoped>

</style>
