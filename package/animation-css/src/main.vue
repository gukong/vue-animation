
/*********************************************/
<!--animated  jello infinite-->
<script>
    import 'animate.css/animate.min.css'
    import AnimationType from './animation-type'

    function isAsyncPlaceholder (node) {
        return node.isComment && node.asyncFactory
    }

    let animationEndListener = null;

    export default {
        name: 'AnimationCss',
        data () {
            return {
                trigger: this.value
            };
        },
        props: {
            animationType: {
                type: String,
                default: ''
            },
            infinite: {
                type: Boolean,
                default: false
            },
            value: {
                type: Boolean,
                default: false
            }
        },
        computed: {
            animatedClass() {
                let dynamicClass = [];
                if (this.trigger) {
                    dynamicClass.push('animated');
                    dynamicClass.push(this.animationType);
                    if (this.infinite) {
                        dynamicClass.push('infinite');
                    }
                }
                return dynamicClass;
            }
        },
        watch: {
            value(val) {
                this.trigger = val;
            }
        },
        mounted() {
            //动画结束时事件
            animationEndListener = () => {
                this.$emit('input', false);
                this.$emit('animation-end')
            };

            this.$nextTick(() => {
                this.$el.addEventListener('webkitAnimationEnd', animationEndListener, false);
            })
        },
        destroyed() {
            this.$el.removeEventListener('webkitAnimationEnd', animationEndListener, false);
        },
        render () {
            let children = this.$options._renderChildren
            if (!children) {
                return
            }

            // filter out text nodes (possible whitespaces)
            children = children.filter((c) => c.tag || isAsyncPlaceholder(c))
            /* istanbul ignore if */
            if (!children.length) {
                return
            }

            // warn multiple elements
            if (children.length > 1) {
                warn(
                    '<transition> can only be used on a single element. Use ' +
                    '<transition-group> for lists.',
                    this.$parent
                )
            }

            const rawChild = children[0]
            rawChild.data.class = this.animatedClass.join(' ');
            return rawChild;
        }
    }
</script>

/*********************************************/

<style lang="scss" rel="stylesheet/scss">

</style>
