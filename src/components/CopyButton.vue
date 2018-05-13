<template>
    <md-button type="button" @click="onClick">Copy!</md-button>
</template>

<script>
import VueClipboard from 'vue-clipboard2';
import Vue from 'vue';

Vue.use(VueClipboard);

export default {
  props: ['data', 'conversor'],
  methods: {
    onClick() {
      const converted = this.conversor(this.data);

      this.$copyText(converted).then(() => {
        this.$emit('copied');
      }, () => {
        this.$emit('error');
      });
    },
  },
};
</script>


<style scoped>
button {
    height: 50px;
    border: 0;
    text-transform: uppercase;

    background: #2ecc71;
    color: white;
    font-size: 18px;
    cursor: pointer;
    margin: 0;
}
</style>
