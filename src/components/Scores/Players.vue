<template>
  <div class="blocks">
    <template v-for="(player, i) in players">
      <Life
        :key="i"
        :playerName="player.name"
        :lifeStatus="player.life"
      />
    </template>
  </div>
</template>

<script>
import Life from './Life';

export default {
  name: 'Players',
  components: {
    Life,
  },
  props: {
    players: Array,
  }
}
</script>

<style lang="scss">
.blocks {
  display: flex;
}
</style>