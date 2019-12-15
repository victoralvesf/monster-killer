<template>
  <div class="container">
    <h4>{{ playerName }}</h4>
    <div class="life-bar">
      <div 
       class="progress"
       :style="{ width: lifeStatus + '%', background: getColor }" />
    </div>
    <span>{{ lifeStatus }}%</span>
  </div>
</template>

<script>
export default {
  name: 'Life',
  props: {
    playerName: String,
    lifeStatus: Number,
  },
  computed: {
    getColor: function() {
      if (this.lifeStatus <= 20) {
        return 'red'
      } else if (this.lifeStatus <= 40) {
        return 'orange'
      } else {
        return 'green'
      }
    }
  }
}
</script>

<style scoped lang="scss">
  div.container {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    max-width: 400px;

    h4 {
      margin: 10px;
      margin-top: 0px;
      font-size: 25px;
    }

    span {
      font-weight: bold;
      margin-top: 8px;
    }
  }

  div.life-bar {
    width: 80%;
    height: 20px;
    border: 1px solid #ccc;
    border-radius: 5px;
    padding: 1px;
    display: grid;
    box-shadow: 0px 1px 3px rgba(#333, 0.15);
  }

  div.progress {
    border-radius: 4px;
    grid-area: 1 / 1;
    transition: .3s all ease;
  }
</style>