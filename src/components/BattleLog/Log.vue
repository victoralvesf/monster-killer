<template>
  <div class="blocks">
    <div class="logs">
      <ul>
        <li v-for="(log, i) in logs"
          :key="i"
          :class="log.css">{{ log.text }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Log',
  props: {
    logs: Array
  }
}
</script>

<style lang="scss" scoped>
  .logs {
    flex-direction: column;
    max-height: 320px;
    overflow-y: auto;
    width: 100%;
  }

  ul {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  li {
    display: block;
    width: 80%;
    padding: 5px;
    font-size: 1rem;
    font-weight: bold;
    color: #fff;
    margin: 3px 0px;
    border-radius: 5px;
    box-shadow: 0px 1px 3px rgba(#000, 0.3);
    text-align: center;
    text-transform: uppercase;
  }

  .player {
    background: rgb(119, 150, 255);
  }

  .monster {
    background: rgb(255, 118, 118);
  }

  .heal {
    background: rgb(0, 200, 0);
  }
</style>