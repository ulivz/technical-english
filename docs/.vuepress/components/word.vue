<template>
  <div class="word">
    <div
      class="word-content"
      :style="{
        borderLeft: `5px solid ${borderColor}`
      }"
    >
      <div class="raw">
        <slot></slot>
      </div>
      <div class="translation">
        <slot name="translation"></slot>
      </div>
    </div>
  </div>
</template>

<script>
  const COLORS = [
    '#3eaf7c',
    '#2c3e50',
    '#DA5961', //#f66
    '#FFE564'
  ]

  export default {
    name: 'word',

    data () {
      return {
        borderColor: COLORS[Math.floor(Math.random() * 4)]
      }
    }
  }
</script>

<style lang="stylus">
  .word
    padding 5px
  .word-content
    padding 10px
    box-sizing border-box
    background-color #f5f5f5
    transition all 0.3s
    &:hover
      background-color: rgba(0, 0, 0, .075)
    .raw
      color #2c3e50
      font-size 24px
      margin-bottom 5px
    .translation
      color lighthen(#2c3e50, 30%)
</style>
