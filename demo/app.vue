<template lang="pug">
.page
  .tab
    a(
      :href="item.link"
      v-for="(item, index) in tabs"
      :class="[{'active': path == item.link}]"
    ) {{item.text}}
  .path {{path}}
</template>

<script>
import annyang from 'annyang'

export default {
  data () {
    return {
      tabs: [
        {text: 'HOME', link: '/home'},
        {text: 'COMMUNITY', link: '/community'},
        {text: 'CART', link: '/cart'},
        {text: 'MINE', link: '/mine'}
      ],
    }
  },

  computed: {
    path: function () {
      return location.pathname
    }
  },

  mounted: function() {
    if (annyang) {
      // Let's define a command.
      const commands = {
        'home': () => location.href = '/home',
        'community': () => location.href = '/community',
        'cart': () => location.href = '/cart',
        'mine': () => location.href = '/mine',
      }
      annyang.debug({newState: true})
      // annyang.setLanguage('zh-CN')

      // Add our commands to annyang
      annyang.addCommands(commands)

      // Start listening.
      annyang.start({ autoRestart: true, continuous: false })
    }
  },



}
</script>

<style lang="stylus" scoped>
.page
  margin 0
  padding 0
.tab
  border 1px solid #ccc
  display flex
  a
    border-right 1px solid #ccc
    flex-grow 1
    text-align center
    padding 5px 0
    color #333
    text-decoration none
    &.active
      background #4bd4a1
      color #fff

.path
  text-align center
  margin-top 50%
</style>