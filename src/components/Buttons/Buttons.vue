<template>
  <div class="blocks">
    <div class="buttons">
      <template v-if="gameIsActive">
        <button class="btn attack" @click="emitEvent('attack')">ataque</button>
        <button class="btn special-attack" @click="emitEvent('special-attack')">ataque especial</button>
        <button class="btn heal" @click="emitEvent('heal')">curar</button>
        <button class="btn give-up" @click="emitEvent('give-up')">desistir</button>
      </template>
      <button v-else class="btn new-game" @click="emitEvent('new-game')">novo jogo</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Buttons',
  props: {
    gameIsActive: Boolean,
  },
  methods: {
    emitEvent(event) {
      this.$emit('clicked', event);
    }
  }
};
</script>

<style lang="scss" scoped>
  .buttons {
    display: flex;
    justify-content: center;

    .btn {
      padding: 5px 15px;
      margin: 0 15px;
      border-radius: 5px;
      border: 0;
      text-transform: uppercase;
      outline: 0;
      font-size: 1.1rem;
      cursor: pointer;
      color: #fff;
      font-weight: 600;
      text-shadow: 0px 2px 2px rgba(#333, 0.8);
    }

    .btn:hover {
      opacity: 0.8;
    }
    
    .attack {
      background: rgb(255, 68, 68);
      box-shadow: 0px 5px 0px rgb(206, 54, 54);
    }

    .special-attack {
      background: orange;
      box-shadow: 0px 5px 0px rgb(201, 131, 0);
    }

    .heal {
      background: green;
      box-shadow: 0px 5px 0px rgb(0, 90, 0);
    }

    .give-up {
      background: gray;
      box-shadow: 0px 5px 0px rgb(82, 81, 81);
    }

    .new-game {
      background: rgb(0, 119, 255);
      box-shadow: 0px 5px 0px rgb(1, 83, 177);
    }
  }
</style>