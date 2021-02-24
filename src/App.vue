<template>
  <div class="app">
    <SMILLoadingIndicator />
    <SkittishButton />
  </div>
</template>

<script>
import SMILLoadingIndicator from './components/SMILLoadingIndicator.vue';
import SkittishButton from './components/SkittishButton.vue';

export default {
  components: { SMILLoadingIndicator, SkittishButton }
}
</script>

<style>
body {
  margin: 0;
  box-sizing: border-box;
  background: slategrey;
  font-family: 'Optima', -apple-system, sans-serif;
}

.app {
  align-items: center;
  display: flex;
  height: 100vh;
  justify-content: space-around;
}
</style>
