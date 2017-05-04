<template>
    <div class="cartcontrol">
        <transition name="move">
            <div class="cart-decrease" v-show="food.count>0" @click="dereaseCart">
                <span class="inner icon-remove_circle_outline"></span>               
            </div>
        </transition>
        <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
        <div class="cart-add icon-add_circle" @click="addCart"></div>
    </div>
</template>

<script>
    import Vue from 'vue';

    export default {
        props: {
            food: {
                type: Object
            }
        },
        created() {

        },
        methods: {
            addCart(event) {
                if (!event._constructed) {
                    return;
                }
                if (!this.food.count) {
                    Vue.set(this.food, 'count', 1);
                } else {
                    this.food.count++;
                }
                // let add = new Vue();
                // add.$emit('cart.add', event.target);
                this.$emit('cart-add', event.target);
            },
            dereaseCart(event) {
                if (!event._constructed) {
                    return;
                }
                if (this.food.count) { 
                    this.food.count--;
                }
            }
        }
    };
</script>

<style lang="stylus" rel="stylesheet/stylus">
    .cartcontrol
        font-size: 0
        .cart-decrease
            display: inline-block
            padding: 6px
            opacity: 1
            .inner
                display: inline-block
                line-height: 24px
                font-size: 24px
                color: rgb(0, 160, 220)
            &.move-enter-active, &.move-leave-active
                transition: all 0.4s linear
                .inner
                    transition: all 0.4s linear
                    transform: ratate(0)
            &.move-enter, &.move-leave
                opacity: 0
                transform: translate3d(24px, 0, 0)
                .inner
                    transform: rotate(180deg)
        .cart-count
            display: inline-block
            vertical-align: top
            width: 12px
            padding-top: 6px
            line-height: 24px
            font-size: 10px
            text-align: center
            color: rgb(147, 143, 159)
        .cart-add
            display: inline-block
            padding: 6px
            line-height: 24px
            font-size: 24px
            color: rgb(0, 160, 220)
</style>
