<template>
  <div v-if="asyncDataStatus_ready" class="col-full push-top">
    <h1>
      Create new thread in <i>{{ forum.name }}</i>
    </h1>

    <ThreadEditor @save="save" @cancel="cancel" />
  </div>
</template>

<script>
import { mapActions } from 'vuex'
import ThreadEditor from '@/components/ThreadEditor.vue'
import asyncDataStatus from '@/mixins/asyncDataStatus'

export default {
  components: {
    ThreadEditor,
  },

  mixins: [asyncDataStatus],

  props: {
    forumId: {
      required: true,
      type: String,
    },
  },
  computed: {
    forum() {
      return this.$store.state.forums[this.forumId]
    },
  },
  methods: {
    ...mapActions(['createThread', 'fetchForum']),

    save({ title, text }) {
      // dispatch action
      this.createThread({
        forumId: this.forum['.key'],
        title,
        text,
      }).then(thread => {
        // After save action redirect to newly created thread
        this.$router.push({
          name: 'ThreadShow',
          params: { id: thread['.key'] },
        })
      })
    },
    cancel() {
      this.$router.push({ name: 'Forum', params: { id: this.forum['.key'] } })
    },
  },

  created() {
    this.fetchForum({ id: this.forumId }).then(() => {
      this.asyncDataStatus_fetched()
    })
  },
}
</script>