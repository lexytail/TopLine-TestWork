<template lang="pug">
div
  ul.comments
    template(v-for="(comment, index) in comments")
      li: comment-item(:comment="comment" @close="onClose(index)")
  p.notification {{ notification }}
</template>

<script lang="ts">
import { Component, Vue, Prop } from "nuxt-property-decorator"
import CommentItem from '~/components/comment/item.vue'

@Component({
  name: 'comment-list',
  components: { CommentItem }
})
export default class extends Vue {

  public notification: string = 'Установка соединения...'

  public requestNumber: number = 0

  public inProccess: number = 0

  public comments: string[] = [
    'МЫ истиная орда!',
    'Сладкий рулет',
    'ВЫ не готовы!',
    'Один туда, другой сюда',
    'Всеищущий путь, выбрал коментарий',
    'Ничего лучше не видел!',
    'Когда у нас уже это появится?',
    'Ахахахахахахаха, понятно',
    'Подскажите с коментарием?',
    'Мне тоже не придумать'
  ]

  public socket: WebSocket = new WebSocket('ws://echo.websocket.org/')

  created() {

    this.socket.onopen = () => this.notification = 'Соединение установлено'

    this.socket.onclose = () => this.notification = ('Соединение закрыто')

    this.socket.onmessage = (event) => {

      if (this.inProccess === -1) { return }

      this.comments.splice(this.inProccess, 1)

      this.inProccess = -1

    }

    this.socket.onerror = (event) => this.notification = event.toString()

  }

  public onClose(index: number) {

    this.inProccess = index

    this.requestNumber++

    this.socket.send(`${this.requestNumber}`)

  }

  
  
  

}
</script>

<style lang="stylus" scoped>
.comments
  border 1px #0bf solid
  border-radius 5px
  padding 1rem
  list-style none

.notification
  text-align center
</style>