<template>
  <div class="header">
    <div class="__contener">
      <div class="head __row">
        <img src="" alt="logo">
        <span>{{NameFile}}</span>
      </div>
      <div class="components __row">
        <span @click="click_block('text')">Text<img src="@/assets/V.svg" alt="V"></span>
        <span @click="click_block('image')">Image<img src="@/assets/V.svg" alt="V"></span>
        <span @click="click_block('forms')">Forms<img src="@/assets/V.svg" alt="V"></span>
        <span @click="click_block('blocks')">Blocks<img src="@/assets/V.svg" alt="V"></span>
        <span @click="click_block('Sliders')">Sliders<img src="@/assets/V.svg" alt="V"></span>
        <span @click="click_block('Custom_component')">Custom component<img src="@/assets/V.svg" alt="V"></span>
        <span @click="click_block('Section')">Section<img src="@/assets/V.svg" alt="V"></span>
      </div>
      <div class="profile">
        <img src="" alt="Profile">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeaderMain",
  props :{
    NameFile : String,
  },
  data () {
    return{}
  }
}
</script>

<style scoped>
.header{
  width: 100%;
  height: 50px;
  background-color: rgba(33, 53, 112, 0.2);
  display: inline-flex;
  padding: 10px;
  justify-content: center;
}
.profile{
  order: 3;
  margin: 0 0 0 0;
}
.components{
  order: 2;
  margin: 0 40px 0 0;
}
.components span{
  font-size: 16px;
  margin: 0 0 0 25px;
}
.components img{
  margin: 0 0 3px 2px;
}
.head{
  order: 1;
  margin: 0 310px 0 0;
}
.head span{
  margin: 0 0 0 155px;
}
.components span:last-child{
  margin: 0 0 0 25px;
}
.components span:first-child{
  margin: 0 25px 0 0;
}
[class*="__contener"]{
  min-width: 1240px;
  display: flex;
  justify-content: center;
  align-items: center;
}
[class*="__col"]{
  flex-direction: column;
}
[class*="__row"]{
  flex-direction: column;
}
</style>