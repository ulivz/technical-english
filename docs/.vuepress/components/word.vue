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
      <a class="redirect-to-google" target="_blank" :href="googleUrl">
        <img src="/google.png" width="16" alt="">
      </a>
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

    mounted () {
      this.raw = this.$el.querySelector('.raw').innerText.trim()
    },

    data () {
      return {
        borderColor: COLORS[Math.floor(Math.random() * 4)],
        raw: null
      }
    },

    computed: {
      googleUrl () {
        return `https://translate.google.com/#auto/zh-CN/${this.raw}`
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
    position relative
    &:hover
      background-color: rgba(0, 0, 0, .075)
    .raw
      color #2c3e50
      font-size 24px
      margin-bottom 5px
    .translation
      color lighthen(#2c3e50, 30%)
    .redirect-to-google
      position absolute
      bottom 5px
      right 5px
</style>
