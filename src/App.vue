<template>
  <header-main   v-bind="this.props"></header-main>
  <div class="bars_position">
    <left-bar></left-bar>
    <WorkSpace :id="component.id" v-for="component in components" :key="component.id">
      <component  v-for="element in component.elements" :key="element.id" :is="component.name">
        <Resize_Block><component :is="element.name"></component></Resize_Block>
      </component>
    </WorkSpace>
    <RightBar></RightBar>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {},

  data () {
    return{ props:{NameFile:"Test"},
      components:[
        {id:1, name: "Section_Block", elements:[{id:1, name:"Text_2_Component"}],
        }
      ],
    }
  },
  methods:{

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
