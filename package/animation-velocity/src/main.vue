<template>
    <div
        @click="triggerClickAnimation"
        @mousedown="triggerMousedownAnimation"
        @mouseup="triggerMouseupAnimation"
        @mouseout="triggerMouseoutAnimation"
        @mouseenter="triggerMouseenterAnimation"
        @mouseover="triggerMouseoverAnimation"
        @mouseleave="triggerMouseleaveAnimation">
        <slot></slot>
    </div>
</template>

/*********************************************/

<script>
    /**

     mouseenter: {},
     mouseout: {},
     mousedown: {},
     mouseup: {},
     click: {}

     trigger: () => {}

     */

    import Velocity from 'velocity-animate';

    function setupVelocityAnimation(el, animations) {
        if (animations) {
            animations.forEach((item) => {
                Velocity(el, item.animation, item.options)
            })
        }
    }

    let mouseupLisener = null;
    export default {
        name: 'AnimationVelocity',
        data () {
            return {
                mousedown: false,
                mouseover: false,
            };
        },
        props: {
            animation: {
                type: Array,
                default: null
            },
            clickAnimation: {
                type: Array,
                default: null
            },
            mouseenterAnimation: {
                type: Array,
                default: null
            },
            mouseoutAnimation: {
                type: Array,
                default: null
            },
            mouseupAnimation: {
                type: Array,
                default: null
            },
            mousedownAnimation: {
                type: Array,
                default: null
            },
            mouseoverAnimation: {
                type: Array,
                default: null
            },
            mouseleaveAnimation: {
                type: Array,
                default: null
            },
            mouseenterWithMousedown: false
        },
        methods: {
            trigger() {
                setupVelocityAnimation(this.$el, this.animation)
            },
            triggerClickAnimation() {
                setupVelocityAnimation(this.$el, this.clickAnimation)
            },
            triggerMouseenterAnimation(event) {
                if (this.mouseenterWithMousedown && !(event.which === 1 && this.mousedown)) {
                    return;
                }
                setupVelocityAnimation(this.$el, this.mouseenterAnimation)
            },
            triggerMouseoutAnimation() {
                setupVelocityAnimation(this.$el, this.mouseoutAnimation)
            },
            triggerMousedownAnimation() {
                this.mousedown = true;
                setupVelocityAnimation(this.$el, this.mousedownAnimation)
            },
            triggerMouseupAnimation() {
                this.mousedown = false;
                setupVelocityAnimation(this.$el, this.mouseupAnimation)
            },
            triggerMouseoverAnimation() {
                if (this.mouseover) {
                    return;
                }
                this.mouseover = true;
                setupVelocityAnimation(this.$el, this.mouseoverAnimation)
            },
            triggerMouseleaveAnimation() {
                this.mouseover = false;
                setupVelocityAnimation(this.$el, this.mouseleaveAnimation)
            }
        },
        mounted() {
            mouseupLisener= (event) => {
                if (!this.$el.contains(event.target)) {
                    this.mousedown = false;
                }
            }
            window.addEventListener('mouseup', mouseupLisener)
        },
        destroyed() {
            window.removeEventListener('mouseup', mouseupLisener)
        }
    }
</script>

/*********************************************/

<style lang="scss" rel="stylesheet/scss">

</style>
