## Install
`npm install vue-animation --save`

## Usage

* css animation

    The animation will be triggered when `value` change to `true`.
    When the animation stoped, `value` will be reset to `false`.
    You'd better to use `v-model`.
     

    AnimationType:
    ```
    AnimationType = {
        BOUNCE: 'bounce',
        FLASH: 'flash',
        PULSE: 'pulse',
        RUBBERBAND: 'rubberBand',
        SHAKE: 'shake',
        HEADSHAKE: 'headShake',
        SWING: 'swing',
        TADA: 'tada',
        WOBBLE: 'wobble',
        JELLO: 'jello',
        HINGE: 'hinge',
    }
    ```
    
    Example:
    ```
    <template>
        <div class="demo-height-root" @click="triggerAction">
            <animation-css
                :animation-type="AnimationType.TADA"
                v-model="trigger">
                <p class="animated-body">案例库抵押后泵</p>
            </animation-css>
        </div>
    </template>
    
    /*********************************************/
    
    <script>
        // Load on demand
        import {AnimationCss, AnimationCssType} from 'vue-animation'
    
        export default {
            components: {
                [AnimationCss.name]: AnimationCss,
            },
            data () {
                return {
                    AnimationType: AnimationCssType,
                    trigger: false
                };
            },
            methods: {
                triggerAction() {
                    this.trigger = true;
                }
            }
        }
    </script>
    ```

* transition animation

    Use this animation with `v-show` or `v-if`.
    You need to set `animation-in-type` and `animation-out-type`. That's all.
    
    AnimationType:
    ```
    AnimationType = {
        BOUNCEIN: 'bounceIn',
            BOUNCEINDOWN: 'bounceInDown',
            BOUNCEINLEFT: 'bounceInLeft',
            BOUNCEINRIGHT: 'bounceInRight',
            BOUNCEINUP: 'bounceInUp',
            BOUNCEOUT: 'bounceOut',
            BOUNCEOUTDOWN: 'bounceOutDown',
            BOUNCEOUTLEFT: 'bounceOutLeft',
            BOUNCEOUTRIGHT: 'bounceOutRight',
            BOUNCEOUTUP: 'bounceOutUp',
            FADEIN: 'fadeIn',
            FADEINDOWN: 'fadeInDown',
            FADEINDOWNBIG: 'fadeInDownBig',
            FADEINLEFT: 'fadeInLeft',
            FADEINLEFTBIG: 'fadeInLeftBig',
            FADEINRIGHT: 'fadeInRight',
            FADEINRIGHTBIG: 'fadeInRightBig',
            FADEINUP: 'fadeInUp',
            FADEINUPBIG: 'fadeInUpBig',
            FADEOUT: 'fadeOut',
            FADEOUTDOWN: 'fadeOutDown',
            FADEOUTDOWNBIG: 'fadeOutDownBig',
            FADEOUTLEFT: 'fadeOutLeft',
            FADEOUTLEFTBIG: 'fadeOutLeftBig',
            FADEOUTRIGHT: 'fadeOutRight',
            FADEOUTRIGHTBIG: 'fadeOutRightBig',
            FADEOUTUP: 'fadeOutUp',
            FADEOUTUPBIG: 'fadeOutUpBig',
            FLIPINX: 'flipInX',
            FLIPINY: 'flipInY',
            FLIPOUTX: 'flipOutX',
            FLIPOUTY: 'flipOutY',
            LIGHTSPEEDIN: 'lightSpeedIn',
            LIGHTSPEEDOUT: 'lightSpeedOut',
            ROTATEIN: 'rotateIn',
            ROTATEINDOWNLEFT: 'rotateInDownLeft',
            ROTATEINDOWNRIGHT: 'rotateInDownRight',
            ROTATEINUPLEFT: 'rotateInUpLeft',
            ROTATEINUPRIGHT: 'rotateInUpRight',
            ROTATEOUT: 'rotateOut',
            ROTATEOUTDOWNLEFT: 'rotateOutDownLeft',
            ROTATEOUTDOWNRIGHT: 'rotateOutDownRight',
            ROTATEOUTUPLEFT: 'rotateOutUpLeft',
            ROTATEOUTUPRIGHT: 'rotateOutUpRight',
            JACKINTHEBOX: 'jackInTheBox',
            ROLLIN: 'rollIn',
            ROLLOUT: 'rollOut',
            ZOOMIN: 'zoomIn',
            ZOOMINDOWN: 'zoomInDown',
            ZOOMINLEFT: 'zoomInLeft',
            ZOOMINRIGHT: 'zoomInRight',
            ZOOMINUP: 'zoomInUp',
            ZOOMOUT: 'zoomOut',
            ZOOMOUTDOWN: 'zoomOutDown',
            ZOOMOUTLEFT: 'zoomOutLeft',
            ZOOMOUTRIGHT: 'zoomOutRight',
            ZOOMOUTUP: 'zoomOutUp',
            SLIDEINDOWN: 'slideInDown',
            SLIDEINLEFT: 'slideInLeft',
            SLIDEINRIGHT: 'slideInRight',
            SLIDEINUP: 'slideInUp',
            SLIDEOUTDOWN: 'slideOutDown',
            SLIDEOUTLEFT: 'slideOutLeft',
            SLIDEOUTRIGHT: 'slideOutRight',
            SLIDEOUTUP: 'slideOutUp',
    }

    ```
    
    Example:
    
    ```
    <template>
        <div class="demo-height-root" @click="rootAction">
            <animation-transition
                :animation-in-type="AnimationType.BOUNCEIN"
                :animation-out-type="AnimationType.BOUNCEOUT">
                <p v-show="show" class="animated-body">案例库抵押后泵</p>
            </animation-transition>
        </div>
    </template>
    
    /*********************************************/
    
    <script>
        import {AnimationVueTransition, AnimationVueTransitionType} from 'vue-animation'
    
        export default {
            components: {
                [AnimationVueTransition.name]: AnimationVueTransition,
            },
            data () {
                return {
                    AnimationType: AnimationVueTransitionType,
                    show: true
                };
            },
            methods: {
                rootAction() {
                    this.show = !this.show;
                }
            }
        }
    </script>

    ```
    
* velocity animation
 
    1, Animations that can be configured:
    ```
    clickAnimation,
    mouseenterAnimation,
    mouseoutAnimation,
    mouseupAnimation,
    mousedownAnimation,
    mouseoverAnimation,
    mouseleaveAnimation,
    ```
    Animations above will be triggered by mouse event. 
    
    2, Another animation:
    ```
    animation    
    ```
    
    The `animation` will not be affected by mouse event. You have to manually trigger it like this `this.$ref.animationRoot.trigger()`
    
    3, If you set `mouseenterWithMousedown` to `true`. Only in the scene below will trigger the `mousedownAnimation`.  
    
    The `mouseenter` event hanppens in the inner of animate element and hold it, then move cursor out of the animate element, continues to hold mouse left button down, move cursor enter the animate element, the `mouseenter` event will be triggered and `mouseenterAnimation` will be triggered. 
    
    How to configure a animation? 
    
    Read the document of [Velocity](http://velocityjs.org) and example below. 

    Example:
    
    ```
    <template>
        <div class="demo-height-root" @click.self="trigger">
            <animation-velocity
                ref="animateRoot"
                :mouseenterWithMousedown="true"
                :animation="animation"
                :mousedownAnimation="mousedownAnimation"
                :mouseupAnimation="mouseupAnimation"
                :mouseenterAnimation="mousedownAnimation"
                :mouseoutAnimation="mouseupAnimation">
                <p class="animated-body">案例库抵押后泵</p>
            </animation-velocity>
        </div>
    </template>
    
    /*********************************************/
    
    <script>
        import {AnimationVelocity} from 'vue-animation'
    
        export default {
            components: {
                [AnimationVelocity.name]: AnimationVelocity,
            },
            data () {
                return {
                    mousedownAnimation: [{
                        animation: {scale: 0.8},
                        options: {duration: 200, queue: false}
                    }],
                    mouseupAnimation: [{
                        animation: {scale: 1},
                        options: {duration: 200, queue: false}
                    }],
                    animation: [{
                        animation: {translateX: '15px', rotateZ: '50deg'},
                        options: {duration: 600}
                    }, {
                        animation: {rotateZ: '100deg'},
                        options: {loop: 2}
                    }, {
                        animation: {
                            rotateZ: '45deg',
                            translateY: '30px',
                            translateX: '30px',
                        }
                    }]
                };
            },
            methods: {
                trigger() {
                    this.$refs.animateRoot.trigger();
                }
            }
        }
    </script>
    ```