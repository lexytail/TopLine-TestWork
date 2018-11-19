<template lang="pug">
div
  .menu
    nuxt-link(to="/one").link Калькулятор дробей
    nuxt-link(to="/two").link WebSocket
  nuxt
</template>

<style lang="stylus" scoped>
.menu
  display flex
  background #09f
  justify-content space-around
  padding .625rem
  margin-bottom 1rem

.link
  background #fff
  border 1px solid #555
  border-radius 5px
  padding .3rem
  text-decoration none
  font 500 1.25rem serif
  color #00f
</style>
