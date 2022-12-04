<template>
  <div class="MovingObject" 
    :style="{
        transform:`translate(${position[0]}px, ${position[1]}px)`, 
        }"></div>
</template>

<script>
export default {
  name: 'MovingObject',
  props: {
    position: Array,
  }
}
</script>

<style scoped>
.MovingObject{
  position: absolute;
    width: 5vw;
    height: calc(5vw * 1.4065);
    max-width: 256px;
    max-height: 360px;
    background-image: url(../assets/img.png);
    background-size: contain;
    display: inline-block;
    box-shadow: 2px 2px 4px 0px #444;
    border-radius: 0.25vw;
    transition: 0.8s cubic-bezier(0.21, 0.29, 0.61, 0.99);
    pointer-events: none;
}
</style>
