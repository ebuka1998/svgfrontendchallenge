<template>
    <svg width="400" height="310" class="animate__animated animate__heartBeat">
        <rect :width="width" :height="height" :fill="color"/>
    </svg>
</template>

<script>
//style="fill:rgb(0,0,255);stroke-width:3;stroke:rgb(0,0,0)"
export default {
    props: ['height', 'color', 'width']
}
</script>


<style>

</style>