<template>
    <canvas id="canvas">

    </canvas>
</template>

<script>
    export default {
        name: '',
        data() {
            return {
                canvas: null,
                windowWidth: document.body.clientWidth
            }
        },
        mounted() {
            const that = this;
            this.$nextTick(() => {
                //获取canvas
                that.canvas = document.getElementById('canvas')
                //监听全局resize事件
                window.onresize = () => {
                    this.windowWidth = document.body.clientWidth
                }

            })
        }
    }
</script>

<style>

</style>
