<template>
    <transition :enter-active-class="enterActiveClass" :leave-active-class="leaveActiveClass" :mode="mode" :appear="appear">
        <slot></slot>
    </transition>
</template>

/*********************************************/
<!--animated  jello infinite-->
<script>
    import 'animate.css/animate.min.css'
    import AnimationType from './animation-type'

    export default {
        name: 'AnimationTransition',
        data () {
            return {
            };
        },
        props: {
            animationInType: {
                type: String,
                default: ''
            },
            animationOutType: {
                type: String,
                default: ''
            },
            mode: '',
            appear: false,
        },
        computed: {
            enterActiveClass() {
                return this.animationInType !== '' ? `animated ${this.animationInType}` : '';
            },
            leaveActiveClass() {
                return this.animationOutType !== '' ? `animated ${this.animationOutType}` : '';
            }
        },
    }
</script>

/*********************************************/

<style lang="scss" rel="stylesheet/scss">

</style>
