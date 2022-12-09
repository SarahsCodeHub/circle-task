<template>
    <div id="canvas">
        <h2>Click inside the box &nbsp;&darr;</h2>
        <div class="box box--dashed" @click="drawCircle" @keydown.stop.prevent="undoLastCircle" tabindex="0"
            style="position: relative">
            <VCircle v-for="([x, y], key) in activeCoords" :key="key" :xCoord="x" :yCoord="y"></VCircle>
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
            stashedCoords: []
        }
    },
    methods: {
        drawCircle(event) {
            const boxLeft = event.target.getBoundingClientRect()?.left
            const boxTop = event.target.getBoundingClientRect()?.top
            const clientX = event.clientX;
            const clientY = event.clientY;
            this.activeCoords.push([clientX - boxLeft, clientY - boxTop])
        },
        undoLastCircle(event) {
            if (event.keyCode == 90 && event.ctrlKey && this.activeCoords.length > 0) {
                const newStashedCircle = this.activeCoords[this.activeCoords.length - 1]
                this.activeCoords.shift();
                this.stashedCoords.push(newStashedCircle);
            }
        }
    },
}
</script>

<style lang="css" scoped>
.box {
    margin: 2rem 4rem;
    min-height: 60vh;
}

.box--dashed {
    border: 1px dashed darkgrey;
    border-radius: .5rem;
}
</style>