<script lang="ts">
import { defineComponent } from 'vue';
// Uncomment import and local "components" registration if library is not registered globally.
// import { VueLibSample } from '@/entry.esm';

export default defineComponent({
  name: 'ServeDev',
  // components: {
  //  VueLibSample,
  // }
});
</script>

<template>
  <div id="app">
    <vue-lib-sample />
  </div>
</template>
