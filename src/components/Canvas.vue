<template>
    <div id="canvas">
        <h2>Click inside the box &nbsp;&darr;</h2>
        <div class="box box--dashed" @click="drawCircle">
            <div v-for="coords in activeCoords" :key="coords.id">
                <VCircle>{{ coords }}</VCircle>
            </div>
        </div>
    </div>
</template>

<script>
import VCircle from "./Circle.vue"

export default {
    name: "VCanvas",
    components: {
        VCircle,
    },
    data() {
        return {
            activeCoords: [],
            stashedCoord: []
        }
    },
    methods: {
        drawCircle(event) {
            this.activeCoords.push([event.offsetX, event.offsetY]);
        }
    },
}
</script>

<style lang="css" scoped>
.box {
    padding: 1.5rem;
    margin: 2rem 4rem;
    min-height: 60vh;
}

.box--dashed {
    border: 1px dashed darkgrey;
    border-radius: .5rem;
}
</style>