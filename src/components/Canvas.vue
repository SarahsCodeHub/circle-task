<template>
    <div id="canvas">
        <h2>Click inside the box &nbsp;&darr;</h2>
        <div class="box box--dashed" @click="drawCircle" @keydown.stop.prevent="redoOrUndoLastCircle" tabindex="0"
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
        undoLastCircle() {
            if (this.activeCoords.length > 0) {
                const newStashedCircle = this.activeCoords[this.activeCoords.length - 1]
                this.activeCoords.shift();
                this.stashedCoords.push(newStashedCircle);
            }
        },
        redoLastCircle() {
            if (this.stashedCoords.length > 0) {
                const redoneCircle = this.stashedCoords[this.stashedCoords.length - 1]
                this.stashedCoords.shift();
                this.activeCoords.push(redoneCircle);
            }
        },
        redoOrUndoLastCircle(event) {
            console.log(event.shiftKey && event.ctrlKey)
            if (!event.ctrlKey) {
                return
            } else if (event.shiftKey && event.ctrlKey && event.keyCode == 90) {
                this.redoLastCircle()
            } else if (event.ctrlKey && event.keyCode === 90) {
                this.undoLastCircle()
            } else {
                return
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