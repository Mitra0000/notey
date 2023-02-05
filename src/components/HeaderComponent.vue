<template>
  <div id="header" class="page-header" style="pointer-events: none;">
    <h1 class="display-1 ms-4">Notey</h1>
  </div>
</template>

<script>

export default {
  name: "HeaderComponent",
}
</script>

<style scoped>
@media screen and (min-width: 600px) {
  #header {
    position: fixed;
    top: 0;
    right: 0;
    left: 0;
    z-index: 1030;
  }
}
</style>