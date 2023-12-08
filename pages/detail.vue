<template>
  <section>
    <v-row>
      <v-col cols="4" v-if="post_detail !== null">
        <v-card class="mx-auto" outlined>
          <v-list-item three-line>
            <v-list-item-content>
              <div class="text-overline mb-4">{{ post_detail.id }}</div>
              <v-list-item-title class="text-h5 mb-1">
                {{ post_detail.title }}
              </v-list-item-title>
              <v-list-item-subtitle>{{
                post_detail.body
              }}</v-list-item-subtitle>
            </v-list-item-content>

            <v-list-item-avatar
              tile
              size="80"
              color="grey"
            ></v-list-item-avatar>
          </v-list-item>

          <v-card-actions>
            <v-btn outlined rounded text> Button </v-btn>
            <v-btn outlined rounded color="primary" @click="updatePost()">
              Update
            </v-btn>
            <v-btn outlined rounded color="error" @click="deletePost()">
              Delete
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
      post_detail: null,
    }
  },

  methods: {
    async getDataDetail() {
      try {
        const id = this.$route.query.id
        console.log(id)
        const res = await this.$axios.get(
          `https://jsonplaceholder.typicode.com/posts/${id}`
        )

        if (res.status === 200) {
          // console.log(res)
          this.post_detail = res.data
        }
      } catch (error) {
        console.error(error)
      }
    },

    //ຟັ່ງຊັນອັບເດດ
    async updatePost() {
      const id = this.$route.query.id
      try {
        const res = await this.$axios.put(
          `https://jsonplaceholder.typicode.com/posts/${id}`,
          {
            userId: 2,
            title: 'Sone SEEDAVANH',
            body: 'SONE SEEDAVANH',
          }
        )

        console.log(res)
        if (res.status === 200) {
          this.getDataDetail()
        }
      } catch (error) {
        console.error(error)
      }
    },

    //ຟັ້ງຊັ່ນລົບ post
    async deletePost() {
      const id = this.$route.query.id
      try {
        const res = await this.$axios.delete(
          `https://jsonplaceholder.typicode.com/posts/${id}`
        )
        console.log(res)
      } catch (error) {
        console.error(error)
      }
    },
  },

  mounted() {
    this.getDataDetail()
  },
}
</script>

<style scoped></style>
