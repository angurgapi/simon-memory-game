<template>
  <div class="game">
    
    <Field />
      
    <div class="start-btn" @click="runGame">{{ runButton }}</div>
    <div class="level">Уровень: {{ this.level }}</div>
    
    <div class="mode">
      <h4>Сложность</h4>
      <button class="mode-btn" v-for="mode, index in this.modes" :key="index" @click="setMode(mode.value)">{{mode.description}}</button>      
    </div>
  </div>
</template>

<script>
import Field from '@/components/Field.vue'
export default {
  name: 'Game',
  components: {
    Field
  },
  data() {
    return {
      runButton: "старт",
      modes: [{value: 'easy', description: 'min', speed: 1500}, {value: 'normal', description: 'mid', speed: 1000}, {value: 'hard', description: 'max', speed: 400}],
      userTurn: false,
      isWon: false,
      gameMode: 'normal',
      level: 0,
      sequence: [],
      sequenceInterval: null,
      userSequence: []      
    }
  },

  mounted: function (){
    document.querySelectorAll('.mode-btn')[1].classList.add('active')
  },
  methods: {
    setMode(mode){
      this.gameMode = mode
      document.querySelectorAll('.mode-btn').forEach(btn => btn.classList.remove('active'))
      event.target.classList.add('active')
    },
    runGame() {
      this.runButton = "начать заново"
      this.isWon = false
      this.level = 1
      clearInterval(this.sequenceInterval)
      this.generateSequence()
    },
    generateSequence() {
      this.sequence = [] 
      this.userSequence = []
      this.userTurn = false
      for (let i=0; i<this.level; i++){
        let randomNum = Math.floor(Math.random() * (4)) + 1
        this.sequence.push(randomNum)             
        }

      let currentMode = this.modes.filter(mode => mode.value === this.gameMode)[0]
      let interval = currentMode.speed
      let currentTile = 0
      this.sequenceInterval = setInterval(() => {   
        if (currentTile >= this.sequence.length) {
          clearInterval(this.sequenceInterval)
          this.userTurn = true
        }     
        if(currentTile < this.sequence.length){
          this.playTile(this.sequence[currentTile])
          currentTile++
        } 
        
      }, interval);

    },

    playTile(tile){     
      this.lightUp(document.querySelectorAll('.tile')[tile-1])
      this.playSound(tile)
      if (this.sequence.length == this.userSequence.length){
        this.checkWin()
      }      
    },
    playSound(n) {     
      let audio = new Audio(require(`@/assets/sounds/${n}.mp3`))     
      audio.play()    
    },
    checkWin() {
      if(JSON.stringify(this.userSequence) === JSON.stringify(this.sequence)){
        this.level++
        this.generateSequence()        
      }      
      else {    
        location.reload()      
        }      
    },
    lightUp(tile) {
      tile.classList.add('activated')
      setTimeout(() => {
         tile.classList.remove('activated')
      }, 300)
    },

  }
}
</script>
<style lang='sass' scoped>
button
  text-transform: uppercase
.start-btn
  display: flex
  align-items: center
  justify-content: center
  margin: 30px auto
  height: 40px
  max-width: 100px
  border: 2px solid #2c3e50
  border-radius: 5px
  box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23)
.mode-btn
  border: 2px solid #2c3e50
  border-radius: 5px
.active
  transform: scale(1.2, 1.2)
  box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23)
  
</style>