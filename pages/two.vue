<template lang="pug">
.page
  h1 WebSocket
  comment-list
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator'
import CommentList from '~/components/comment/list.vue'

@Component({
  components: { CommentList }
})
export default class extends Vue {

}
</script>
