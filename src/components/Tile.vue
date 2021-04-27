<template>
  <div class="tile">
    <button ref="btn" :style="`background-color:${color}`" @click='playTile(value)' :data-tile="value">       
    </button>  
  </div>
</template>

<script>
export default {
  name: 'tile',
  props: {   
    value: {
      type: String,
      required: true
    },
    color: {
      type: String,
      required: true
    }
  }, 
  methods: {
    playTile (tile) {
      if(this.$parent.$parent.userTurn){
        this.$parent.$parent.userSequence.push(parseInt(tile))   
        this.$parent.$parent.playTile(tile)
      }
      
    }
  }
}
</script>

<style scoped lang="sass">

  .tile 
    outline: none
    opacity: .6
    user-selection: none
    animation: effect_dylan 800ms
    -webkit-tap-highlight-color: transparent 
    button
      position: relative
      display: inline-block
      cursor: pointer
      margin: 0 auto
      width: 60px
      height: 60px
      outline: none
      transition: all 100ms ease-in
      color: #ffffff
      font-weight: 700
      opacity: .6
      cursor: pointer
      border: dotted 1px transparent
      box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23)     
      &.click 
        opacity: 1
        pointer-events: none
        user-select: none

  .activated
    opacity: 1
  
</style>