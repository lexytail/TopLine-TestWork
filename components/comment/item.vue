<template lang="pug">
div.comment
  button(@click="close").close x
  span {{ comment }}
</template>

<script lang="ts">
import { Component, Vue, Prop } from "nuxt-property-decorator"

@Component({ name: 'comment-list' })
export default class extends Vue {

  @Prop()
  public comment?: string



  close(index: number) {

    this.$emit('close')

  }

}
</script>

<style lang="stylus" scoped>
.comment
  display flex
  align-items center
  margin-bottom .75rem

  > .close
    outline none
    border-radius 50%
    border none
    cursor pointer
    margin 0 .5rem

    &:active
      background #0bf
</style>