<template>
    <div @dblclick="click_on" id="block" class="block">
      <div @mousedown="click_in_block('up')" @mouseup="up_in_block" class="up"></div>
      <div @mousedown="click_in_block('left')" @mouseup="up_in_block" class="left"></div>
      <div @mousedown="click_in_block('right')" @mouseup="up_in_block" class="right"></div>
      <div @mousedown="click_in_block('right-top')" @mouseup="up_in_block" class="right-top"></div>
      <div @mousedown="click_in_block('left-top')" @mouseup="up_in_block" class="left-top"></div>
      <div @mousedown="click_in_block('move')" @mouseup="up_in_block"  class="slot">
       <slot></slot>
      </div>
      <div @mousedown="click_in_block('down')" @mouseup="up_in_block" class="down"></div>
      <div @mousedown="click_in_block('right-bottom')" @mouseup="up_in_block" class="right-bottom"></div>
      <div @mousedown="click_in_block('left-bottom')" @mouseup="up_in_block" class="left-bottom"></div>
    </div>
</template>

<script>
export default {
  name: "Resize_Block",
  data(){
    return{X: 0, Y: 0, height_block: 0, width_block: 0,direction: "", margin_bottom: 0, margin_left: 0, margin_right: 0, margin_top: 0,click: false}
  },
  props:['id'],
  mounted() {
    console.log(this.id);
    console.log(this.$props.id);
    this.$el.setAttribute('id', 'block' + this.id);
  },
  methods:{
    click_on(){
      let child = document.getElementById("block" + this.id).children;
      if(this.click == false){
        this.click = true;
        child[0].style.display = "block";
        child[1].style.display = "block";
        child[2].style.display = "block";
        child[3].style.display = "block";
        child[4].style.display = "block";
        child[6].style.display = "block";
        child[7].style.display = "block";
        child[8].style.display = "block";
        child[9].style.display = "block";
        child[5].style.cursor = "move";
      }else{
        this.click = false;
        child[0].style.display = "none";
        child[1].style.display = "none";
        child[2].style.display = "none";
        child[3].style.display = "none";
        child[4].style.display = "none";
        child[6].style.display = "none";
        child[7].style.display = "none";
        child[8].style.display = "none";
        child[9].style.display = "none";
        child[5].style.cursor = "default";
      }
    },
    click_in_block(e) {
      if(this.click == true){
        let el = document.getElementById("block" + this.id);
        this.X = event.clientX;
        this.Y = event.clientY;
        this.height_block = el.offsetHeight;
        this.width_block = el.offsetWidth;
        this.margin_top = window.getComputedStyle(el).getPropertyValue("margin-top").replace("px","");
        this.margin_right = window.getComputedStyle(el).getPropertyValue("margin-right").replace("px","");
        this.margin_left = window.getComputedStyle(el).getPropertyValue("margin-left").replace("px","");
        this.margin_bottom = window.getComputedStyle(el).getPropertyValue("margin-bottom").replace("px","");
        this.direction = e;
        document.getElementById("site").addEventListener("mousemove", this.mouseMove);
      }
    },
    up_in_block(){
      document.getElementById("site").removeEventListener("mousemove", this.mouseMove);
    },
    mouseMove() {
        let el = document.getElementById("block" + this.id);
        switch (this.direction){
          case "up":{
            el.style.marginTop = Number(this.margin_top - Number(this.Y - event.pageY)) + "px";
            el.style.height = Number(this.height_block + Number(this.Y - event.pageY)) + "px";
            break;
          }
          case "down":{
            el.style.marginBottom = Number(this.margin_bottom - Number(event.pageY - this.Y)) + "px";
            el.style.height = Number(this.height_block + Number( event.pageY - this.Y)) + "px";
            break;
          }
          case "left":{
            el.style.marginLeft = Number(this.margin_left - Number(this.X - event.pageX)) + "px";
            el.style.width = Number(this.width_block + Number(this.X - event.pageX)) + "px";
            break;
          }
          case "right":{
            el.style.marginRight = Number(this.margin_right - Number( event.pageX - this.X)) + "px";
            el.style.width = Number(this.width_block + Number(event.pageX - this.X)) + "px";
            break;
          }
          case "move":{
            if(this.X > event.pageX){
              el.style.marginLeft = this.margin_left - Number(this.X - event.pageX) + 'px';
              el.style.marginRight = Number(Number(this.margin_right) + Number(this.X - event.pageX)) + 'px';
            }
            if(this.X < event.pageX){
              el.style.marginRight = this.margin_right - Number(event.pageX - this.X) + 'px';
              el.style.marginLeft = Number(Number(this.margin_left) + Number(event.pageX - this.X)) + 'px';
            }
            if(this.Y > event.pageY){
              el.style.marginTop = this.margin_top - Number(this.Y - event.pageY) + 'px';
              el.style.marginBottom = Number(Number(this.margin_bottom) + Number(this.Y - event.pageY)) + 'px';
            }
            if(this.Y < event.pageY){
              el.style.marginBottom = this.margin_bottom - Number(event.pageY - this.Y) + 'px';
              el.style.marginTop = Number(Number(this.margin_top) + Number(event.pageY - this.Y)) + 'px';
            }
          }
          // case "left-top" :{
          //
          // }
        }
    },
  }
}
</script>

<style scoped>
.block{
  height: auto;
  position: relative;
  width: auto;
  min-width: 20px;
  min-height: 20px;
  margin: auto;
  user-select: none;
}
.slot{
  width: 100%;
  height: 100%;
  cursor: default;
}
.right-bottom{
  background-color: white;
  border-radius: 50%;
  border: 2px solid rgb(40, 198, 246);
  width: 10px;
  z-index: 15;
  display: none;
  height: 10px;
  position: absolute;
  bottom: -5px;
  right: -5px;
}
.left-bottom{
  background-color: white;
  border-radius: 50%;
  border: 2px solid rgb(40, 198, 246);
  width: 10px;
  display: none;
  z-index: 15;
  height: 10px;
  position: absolute;
  bottom: -5px;
  left: -5px;
}
.right-top{
  background-color: white;
  border-radius: 50%;
  border: 2px solid rgb(40, 198, 246);
  width: 10px;
  display: none;
  z-index: 15;
  height: 10px;
  position: absolute;
  top: -5px;
  right: -5px;
}
.left-top{
  border-radius: 50%;
  background-color: white;
  border: 2px solid rgb(40, 198, 246);
  width: 10px;
  display: none;
  z-index: 15;
  height: 10px;
  position: absolute;
  top: -5px;
  left: -5px;
}
.up{
  position: absolute;
  display: none;
  top: 0;
  z-index: 9;
  cursor: ns-resize;
  width: 100%;
  height: 3px;
  background-color: rgba(76, 255, 83, 1);
  margin: 0 0 0 0;
}
.down{
  position: absolute;
  bottom: 0;
  display: none;
  z-index: 9;
  cursor: ns-resize;
  width: 100%;
  height: 3px;
  background-color: rgba(76, 255, 83, 1);
  margin: 0 0 0 0;
}
.left{
  cursor: ew-resize;
  width: 3px;
  display: none;
  z-index: 9;
  height: 100%;
  float: left;
  background-color: rgba(76, 255, 83, 1);
  margin: 0 0 0 0;
}
.right{
  cursor: ew-resize;
  width: 3px;
  display: none;
  z-index: 9;
  float: right;
  height: 100%;
  background-color: rgba(76, 255, 83, 1);
  margin: 0 0 0 0;
}
</style>