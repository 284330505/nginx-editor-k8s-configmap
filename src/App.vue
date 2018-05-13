<template>
  <div id="app">

    <div class="container">
      <Editor @copied="onCopied" :conversor="toPretty" @dataChange="onDataChange"></Editor>
      <CopyButton :data="data" :conversor="toUgly" @copied="onCopied"></CopyButton>
    </div>

    <Snackbar :show="showSnackbar" @closed="showSnackbar = false"></Snackbar>
  </div>
</template>

<script>
import Editor from './components/Editor';
import Snackbar from './components/Snackbar';
import CopyButton from './components/CopyButton';

export default {
  name: 'App',
  components: {
    Editor,
    CopyButton,
    Snackbar,
  },
  data() {
    return {
      data: '',
      showSnackbar: false,
    };
  },
  methods: {
    onDataChange(data) {
      this.data = data;
    },
    onCopied() {
      this.showSnackbar = true;
    },
    toUgly(data) {
      return data.replace(/\n/g, '\\n')
        .replace(/\t/g, '\\t')
        .replace(/"/g, '\\"');
    },
    toPretty(data) {
      // TODO:
      // add more conversions as we move along
      return data.replace(/\\n/g, '\n')
        .replace(/\\t/g, '\t')
        .replace(/\\"/g, '"');
    },
  },
};
</script>

<style>
html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}

html {
  height: 100%;
}
body {
  margin: 0;
  height: 100%;
  display: flex;
}

#app {
  display: flex;
  flex: 1;
}

.container {
  display: flex;
  flex-direction: column;
  flex: 1;
}
</style>
