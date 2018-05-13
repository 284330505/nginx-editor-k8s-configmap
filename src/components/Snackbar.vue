<template>
    <md-snackbar class="md-snackbar-top md-snackbar-right"
                 :md-position="'left'"
                 :md-duration="2000"
                 :md-active.sync="showInternal"
                 @md-closed="$emit('closed');">
        <span>Copied to clipboard!</span>
    </md-snackbar>
</template>

<script>
import Vue from 'vue';
import VueMaterial from 'vue-material';
import 'vue-material/dist/vue-material.min.css';

Vue.use(VueMaterial);

// We need to maintain an internal flag
// Since :md-active.sync modifies the argument
// And md-closed doesn't work without md-active.sync :)
export default {
  props: ['show'],
  data() {
    return {
      showInternal: false,
    };
  },
  watch: {
    show(newValue) {
      if (newValue) {
        this.showInternal = true;
      }
    },
  },
};
</script>


<style>
.md-snackbar {
  background-color: #e67e22;
  color: #fff;
}

/* Move the snackbar to the top right */
.md-snackbar-right.md-snackbar {
  right: 24px;
  left: initial !important;
}

.md-snackbar-top.md-snackbar {
  top: 24px;
  bottom: initial !important;
}

.md-snackbar-top.md-snackbar-enter,
.md-snackbar-top.md-snackbar-leave-active {
  transform: translate3D(0, calc(-100% + -8px), 0) !important;
}
</style>
