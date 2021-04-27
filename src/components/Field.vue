<template>
  <div class="field">
    <Tile :value="'1'" :color="'#144722'" />
    <Tile :value="'2'" :color="'#f5bd07'" />
    <Tile :value="'3'" :color="'#47090b'" />
    <Tile :value="'4'" :color="'#040d3d'" />
  </div>
</template>

<script>
import Tile from '@/components/Tile.vue'
export default {
  name: 'Field',
  components: {
    Tile
  },
}
</script>

<style scoped lang="sass">
  .field 
    display: grid
    grid-template-rows: repeat(2, auto)
    grid-template-columns: repeat(2, auto)
    width: 100%    
    grid-gap: 20px
    background-color: #ffffff
    align-items: center
    justify-content: center
    border-radius: 8px
    
</style>