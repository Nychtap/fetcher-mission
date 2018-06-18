<template>
  <div class="txt">
    <h1>{{ txt }}</h1>
  </div>
</template>

<script>
export default {
  props: {
    txt: String,
  }
}

</script>
<style lang="css">
.txt {
  height: auto;
  width: 100%;
  position: fixed;
  background-color: gray;
  color: white;
}
</style>
