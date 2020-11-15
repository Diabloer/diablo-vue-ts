<template>
<button class="gulu-switch" :class="{'gulu-switch__checked':value}" @click="toggle"><span></span></button>
</template>

<script lang="ts">
import {
    ref
} from 'vue'
export default {
    props: {
        value: Boolean
    },
    setup(props, context) {
        const toggle = () => {
            context.emit('update:value', !props.value)
        }
        return {
            toggle
        }
    }
}
</script>

<style lang="scss">
$h: 22px;
$h2: $h - 4px;

.gulu-switch {
    height: $h;
    width: $h*2;
    border: none;
    background: #bfbfbf;
    border-radius: $h/2;
    position: relative;

    >span {
        position: absolute;
        top: 2px;
        left: 2px;
        height: $h2;
        width: $h2;
        background: white;
        border-radius: $h/2;
        transition: all 0.2s;
    }

    &:focus {
        outline: none;
    }

    &.gulu-switch__checked {
        background: #1890ff;
    }

    &.gulu-switch__checked>span {
        left: calc(100% - #{$h2} - 2px);
    }

    &:active {
        >span {
            width: $h2 + 4px;
        }
    }

    &.gulu-switch__checked:active {
        >span {
            width: $h2 + 4px;
            margin-left: -4px;
        }
    }
}
</style>
