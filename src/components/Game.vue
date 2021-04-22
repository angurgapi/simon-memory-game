<template>
  <div class="game">
    <h1>level {{ lvl }}</h1>
    <p>
      difficulty
    </p>
    
  </div>
</template>

<script>
export default {
  name: 'Game',
  props: {
    lvl: Number
  }
}
</script>
<style lang='sass' scoped>
.game
  background-color: rgba(0,0,0,.3)
</style>