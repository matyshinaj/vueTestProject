<template>
  <div class="logo">
    <img class="img-logo" src="../assets/logo.png" />
  </div>
</template>
<script>
export default {
  name: "Logo",
};
</script>
<style>
.logo {
  position: fixed;
  bottom: 0px;
  right: 0px;
  height: 60px;
}
.img-logo {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
}
</style>
