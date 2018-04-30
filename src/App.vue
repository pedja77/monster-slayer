<template>
  <div id="app" >
    <section class="row">
        <HealthBar player="You" :health="playersHealth"/>
        <HealthBar player="Monster" :health="monstersHealth"/>
    </section>
    <section class="row controls" v-if="!isGameRunning" >
        <div class="small-12 columns" >
            <MSButton id="start-game" caption="START NEW GAME" action="start" @start="handleStartGame"/>
        </div>
    </section>
    <section class="row controls" v-if="isGameRunning">
        <div class="small-12 columns">
            <MSButton id="attack" caption="ATTACK" action="attack" @attack="handleAttack" />
            <MSButton id="special-attack" 
                caption="SPECIAL ATTACK" 
                action="special-attack" 
                @special-attack="handleAttack(true)"/>
            <MSButton id="heal" caption="HEAL" action="heal" @heal="handleHeal"/>
            <MSButton id="give-up" caption="GIVE UP" action="give-up" @give-up="handleGiveUp"/>
        </div>
    </section>
    <section class="row log">
        <Logs :logs="logs"/>
    </section>
</div>
</template>

<script>
import HealthBar from './components/HealthBar.vue'
import MSButton from './components/MSButton.vue'
import Logs from './components/Logs.vue'

const healingValue = 15

export default {
  name: 'app',
  components: {
    HealthBar,
    MSButton,
    Logs
  },
  data() {
      return {
          isGameRunning: false,
          playersHealth: 45,
          monstersHealth: 63,
          logs: []
      }
  },
  methods: {
      handleStartGame(value) {
          this.isGameRunning = true
          this.playersHealth = 100
          this.monstersHealth = 100
          this.logs = []
          //this.logs.unshift('Game started')
      },
      handleAttack(special = false) {
          let playersAttack = special ? 10 : Math.floor(Math.random() * 10 + 1)
          let monstersAttack = this.monstersTurn()
          this.monstersHealth -= playersAttack
          this.playersHealth -= monstersAttack
          this.logs.unshift({
               'player':`You hit monster for ${playersAttack} damage`,
               'monster': `Monster hits you for ${monstersAttack} damage`
               })
          
          if (this.playersHealth <= 0 || this.monstersHealth <= 0) {
              let winner = this.playersHealth <= 0 ? 'Monster' : 'You'
              alert(winner + " won!")
              this.isGameRunning = false
          }
      },
      
      handleHeal() {
          this.playersHealth += healingValue
          let monstersAttack = this.monstersTurn()
          this.playersHealth -= monstersAttack
          this.logs.unshift({
               'player':`You healed for ${healingValue} hit points`,
               'monster': `Monster hits you for ${monstersAttack} damage`
               })
          
          if (this.playersHealth <= 0 || this.monstersHealth <= 0) {
              let winner = this.playersHealth <= 0 ? 'Monster' : 'You'
              alert(winner + " won!")
              this.isGameRunning = false
          }
      },
      handleGiveUp() {
          this.logs.unshift({player: 'You run away!!'})
          alert('You run away! Monster won!')
          this.isGameRunning = false
      },
      monstersTurn() {
          let dmg = Math.floor(Math.random() * 10 + 1)
          //this.playersHealth -= dmg
          return dmg
      }
  }
}
</script>


