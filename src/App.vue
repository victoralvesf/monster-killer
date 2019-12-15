<template>
  <div id="app">
    <h1>Matador de Monstro</h1>
    <Players :players="players" />
    <Result v-if="hasResult" :win="winnerResult" />
    <Buttons @clicked="playerClick" :gameIsActive="gameIsActive" />
    <Log v-if="logs.length" :logs="logs" />
  </div>
</template>

<script>
import Players from './components/Scores/Players';
import Result from './components/Result/Result';
import Buttons from './components/Buttons/Buttons';
import Log from './components/BattleLog/Log';

export default {
  name: 'app',
  components: {
    Players,
    Result,
    Buttons,
    Log,
  },
  data() {
    return {
      players: [
        { name: 'Jogador', life: 100 },
        { name: 'Monstro', life: 100 },
      ],
      gameIsActive: false,
      logs: [],
      actions: {
        'new-game': () => {
          this.startGame();
        },
        'attack': () => {
          this.attack(false);
        },
        'special-attack': () => {
          this.attack(true);
        },
        'heal': () => {
          this.healAndHurt();
        },
        'give-up': () => {
          this.giveUp();
        }
      }
    }
  },
  computed: {
    hasResult() {
      return this.players[0].life == 0 || this.players[1].life == 0
    },
    winnerResult() {
      return this.players[0].life !== 0 && this.players[1].life == 0
    },
  },
  methods: {
    playerClick(event) {
      this.actions[event]();
    },
    resetLife() {
      this.players.map((item) => {
        item.life = 100;
      });
    },
    startGame() {
      this.gameIsActive = true;
      this.logs = []
      this.resetLife();
    },
    giveUp() {
      this.gameIsActive = false;
      this.logs = [];
    },
    attack(special) {
      this.hurt(1, 5, 10, special, 'Jogador', 'Monstro', 'player');
      if(this.players[1].life > 0) {
        this.hurt(0, 7, 12, false, 'Monstro', 'Jogador', 'monster');
      }
    },
    hurt(player, min, max, special, source, target, _class) {
      const plus = special ? 5 : 0;
      const hurt = this.getRandom(min + plus, max + plus);
      this.players[player].life = Math.max(this.players[player].life - hurt, 0);
      this.registerLog(`${source} atingiu ${target} com ${hurt} de dano.`, _class);
    },
    healAndHurt() {
      this.heal(10, 15);
      this.hurt(0, 7, 12, false, 'Monstro', 'Jogador', 'monster');
    },
    heal(min, max) {
      const heal = this.getRandom(min, max);
      this.players[0].life = Math.min(this.players[0].life + heal, 100);
      this.registerLog(`Jogador recebeu ${heal} de cura.`, 'heal');
    },
    getRandom(min, max) {
      const value = Math.random() * (max - min) + min;
      return Math.round(value);
    },
    registerLog(text, css) {
      this.logs.unshift({ text, css });
    }
  },
  watch: {
    hasResult(value) {
      if (value) this.gameIsActive = false;
    }
  }
}
</script>

<style lang="scss">
  body {
    padding: 0;
    margin: 0;
    background: rgba(#000, 0.1);
  }

  #app {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100vh;

    h1 {
      font-weight: bold;
      font-size: 3rem;
      margin: 15px 0px 0px 0px;
    }
  }

  .blocks {
    display: flex;
    justify-content: space-around;
    width: 90vw;
    max-width: 968px;
    border: 1px solid #eee;
    padding: 30px;
    border-radius: 5px;
    box-shadow: 0px 1px 3px rgba(#000, 0.2);
    margin: 6px;
    background: #fff;
  }
</style>
