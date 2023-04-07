<template>
  <header-main @update:create_component="this.create_component = $event" @click_create_component="create_components()" v-bind="this.props"></header-main>
  <div class="bars_position">
    <left-bar></left-bar>
    <WorkSpace :id="component.id" v-for="component in components" :key="component.id">
      <component  :is="component.name">
        <Resize_Block v-for="element in component.elements" :key="element.id"><component :id="element.id" :is="element.name"></component></Resize_Block>
      </component>
    </WorkSpace>
    <RightBar>
    </RightBar>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return{ props:{NameFile:"Test"},
      create_component: "",
      components:[
        {id: 1, name: "Section_Block", elements:[{id: 1, name:"Text_1_Component"}],
        }
      ],
    }
  },
  methods:{
    create_components(){
      for(let i=0;i<this.components.length;i++){
        if(this.components[i].name == "Section_Block"){
          let id = this.components[i].elements[this.components[i].elements.length - 1].id;
          let object = {id: id + 1, name: this.create_component};
          this.components[i].elements.push(object);
          this.create_component = "";
        }
      }
    }
  }
}
</script>

<style>
body{
    margin: 0;
    padding: 0;
    font-family: Josefin_Sans;
    min-width: 100%;
}
.bars_position{
  display: flex;
  flex-direction: row;
}
.bars_position:first-child{
    order: 1;
    margin: 0 0 0 0;
}
.bars_position:last-child{
    order: 3;
    margin: 0 0 0 0;
}
@font-face {
   font-family: Josefin_Sans;
   src: url("Fonts/Josefin_Sans/JosefinSans-VariableFont_wght.ttf");
}
</style>
