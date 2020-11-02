<template>
    <svg height="250" width="500" class="animate__animated animate__backInDown">
        <polygon :points="points" :fill="color" />
    </svg>  
</template>

<script>
//220,10 300,210 170,250 123,234
export default {
    props: ['points', 'color']
}
</script>

<style>

</style>