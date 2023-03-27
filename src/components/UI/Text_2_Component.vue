<template>
  <h2 @click="input" >Your text</h2>
</template>

<script>
export default {
  name: "Text_2_Component",
  methods:{
    input(){
      document.addEventListener("keydown", this.press_keyboard);
    },
    press_keyboard(e){
        console.log(e);
        if(e.key == "Escape"){
          document.removeEventListener("keydown", this.press_keyboard);
        }else if(e.key == "Backspace"){
          console.log(this.$el.innerText);
          this.$el.innerText = this.$el.innerText.substring(0, this.$el.innerText.length - 1 );
        }else if(e.key == "Enter"){
          this.$el.innerText += "\n";
        }
        else{
          this.$el.innerText += e.key;
        }
    }
  },
}
</script>

<style scoped>

</style>