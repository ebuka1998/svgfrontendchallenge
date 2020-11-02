<template>
  <div>
    <svg width="500" height="500" class="animate__animated animate__backInDown">
        <circle cx="100" cy="100" :r="radius"  stroke-width="4" :fill="color" />
    </svg>
  </div>
</template>

<script>
export default {
  props: ['radius', 'color']
}
</script>

<style>

</style>