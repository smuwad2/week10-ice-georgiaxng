<script>
export default {
  data() {
    return {
      soundLevel: 0
    };
  },
  computed: {
    soundIcon() {
      switch (this.soundLevel) {
        case 0:
          return '🔇';
        case 1:
          return '🔈';
        case 2:
          return '🔉';
        case 3:
          return '🔊';
        default:
          return '';
      }
    }
  }
};
</script>

<template>
  <div>
    <label>
      Sound level
      <input type="number" min="0" max="3" v-model="soundLevel" />
    </label>
    <span>{{ soundIcon }}</span>
  </div>
</template>


