<template>
    <div data-is-badge v-if="number > 0 || dot" :data-props-dot="dot">
        <span v-if="!dot">{{limit(number, maxDigits)}}</span>
    </div>
</template>
<script>
import times from 'lodash/times'
export default {
    name: 'badge',
    prefix: 'sa',
    props: {
        number: {
            type: Number,
            default: 0
        },
        maxDigits: {
            type: Number,
            default: 2
        },
        dot: {
            type: Boolean,
            default: false
        }
    },
    methods:{ 
        limit(number, maxDigits) {
            if(number >= Math.pow(10, maxDigits)) {
                return times(maxDigits, ()=>9).join('')+'+'
            }
            return number
        }
    }
}
</script>
<style>
[data-is-badge] {
    height: 20px;
    display: inline-block;
    min-width: 20px;
    border-radius: 10px;
    line-height: 20px;
    font-size: 12px;
    background: #fd5555;
    color: white;
    text-align: center;
    padding: 0 6px;
}
[data-props-dot] {
    width: 7px;
    height: 7px;
    border-radius: 50%;
    min-width: initial;
    padding: 0;
}
</style>
