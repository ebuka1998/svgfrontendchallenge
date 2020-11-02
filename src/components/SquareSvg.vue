<template>
  <svg width="400" height="400" class="animate__animated animate__backInRight">
  <rect x="50" y="20" :width="width" :height="height" :fill="color"/>
</svg>
</template>

<script>
//style="stroke:pink;stroke-width:5;fill-opacity:0.1;stroke-opacity:0.9"
export default {
  props: ['height', 'color', 'width']
}
</script>

<style>

</style>