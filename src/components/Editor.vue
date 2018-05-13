<template>
  <codemirror v-model="code"
    :options="cmOptions"
    @inputRead="onNewInput"
    @input="onInput"></codemirror>
</template>

<script>
import { codemirror } from 'vue-codemirror';

import 'codemirror/lib/codemirror.css'; // eslint-disable-line
import 'codemirror/theme/lucario.css'; // eslint-disable-line
import 'codemirror/mode/nginx/nginx'; // eslint-disable-line

export default {
  props: ['conversor'],
  components: {
    codemirror,
  },
  data() {
    return {
      code: '',
      cmOptions: {
        tabSize: 4,
        mode: 'text/x-nginx-conf',
        theme: 'lucario',
        lineNumbers: true,
        lineWrapping: true,
        line: true,
      },
    };
  },
  methods: {
    onNewInput(codeMirror, newInput) {
      if (newInput.origin === 'paste') {
        const value = this.conversor(codeMirror.getValue());

        codeMirror.setValue(value);
      }
    },
    onInput(value) {
      this.$emit('dataChange', value);
    },
  },
};
</script>

<style>
.vue-codemirror {
  flex: 1;
  display: flex;
  max-width: 100vw;
}
.CodeMirror {
  flex: 1;
  height: auto;
}
</style>
