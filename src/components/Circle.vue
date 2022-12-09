<template>
    <div style="position: absolute; font-size: 2rem; cursor: crosshair" :title="`[x: ${xCoord}, y:${yCoord}]`"
        :style="{ left: xCoord + 'px', top: yCoord + 'px' }">
        &#8859;
    </div>
</template>

<script>
export default {
    name: "VCircle",
    props: {
        xCoord: {
            type: Number
        },
        yCoord: {
            type: Number
        }
    },
}
</script>

<style lang="scss" scoped>

</style>