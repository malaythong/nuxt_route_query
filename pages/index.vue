<template>
  <section>
    <v-row>
      <v-col cols="3" v-for="(post, index) in posts" :key="`post-${index}`">
        <v-card class="mx-auto" outlined>
          <v-list-item three-line>
            <v-list-item-content>
              <div class="text-overline mb-4">{{ post.id }}</div>
              <v-list-item-title class="text-h5 mb-1">
                Headline 5
              </v-list-item-title>
              <v-list-item-subtitle>{{ post.body }}</v-list-item-subtitle>
            </v-list-item-content>

            <v-list-item-avatar
              tile
              size="80"
              color="grey"
            ></v-list-item-avatar>
          </v-list-item>

          <v-card-actions>
            <v-btn outlined rounded text :to="`/detail?id=${post.id}`">
              Button
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </section>
</template>

<script>
export default {
  data() {
    return {
      posts: [],
    }
  },

  methods: {
    async getData() {
      try {
        const res = await this.$axios.get(
          'https://jsonplaceholder.typicode.com/posts'
        )

        console.log(res)
        if (res.status === 200) {
          this.posts = res.data
        }
      } catch (error) {
        console.error(error)
      }
    },
  },

  mounted() {
    this.getData()
  },
}
</script>
