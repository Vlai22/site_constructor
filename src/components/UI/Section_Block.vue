<template>
    <section class="section">
          <slot></slot>
    </section>
</template>

<script>
export default {
  name: "Section_Block"
}
</script>

<style scoped>
.section{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
}
.test{
  background-color: green;
  width: 1000px;
  height: 500px;
}
</style>