<template>
  <div class="space">
    <div id="site" class="site">
        <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "WorkSpace"
}
</script>

<style scoped>
.space{
  width: auto;
  overflow: auto;
  height: auto;
  margin: 0;
  padding: 0;
  border: 0;
  flex: 2 0 auto;
  background-color: rgb(147, 99, 99);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.site{
  display: flex;
  flex-direction: column;
  margin: 0;
  padding: 0;
  width: 1080px;
  background-color: rgba(148, 228, 238, 1);
  height: 100vh;
}
</style>