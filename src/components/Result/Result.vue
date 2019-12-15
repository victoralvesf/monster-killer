<template>
  <div class="blocks">
    <span v-if="win" :class="{ winner : win }">Você ganhou!! :D</span>
    <span v-else>Você perdeu! :(</span>
  </div>
</template>

<script>
export default {
  name: 'Result',
  props: {
    win: Boolean,
  }
}
</script>

<style lang="scss" scoped>
  span {
    font-size: 1.7rem;
    font-weight: bold;
    color: red;
  }

  span.winner {
    color: green;
  }
</style>