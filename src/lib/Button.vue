<template>
<button class="gulu-button" :class="classes">
    <slot />
</button>
</template>

<script lang="ts">
import { computed } from 'vue'
export default {
    // 1. props 需要先声明才能取值，attrs 不用申明
    // 2. props 不包含事件，attrs 包含
    // 3. props 没有申明属性，会跑到 attrs 中
    // 4. props 支持 string 以外的类型，attrs 只有 string 类型
    props: {
        theme: {
            type: String,
            default: "button"
        },
        size: {
            type: String,
            default: "normal"
        }
    },
    setup(props, context) {
        const { theme, size } = props;
        const classes = computed(() => {
            return {
                [`gulu-theme-${theme}`]: theme,
                [`gulu-size-${size}`]: size
            };
        });
        return { classes };
    }
}
</script>

<style lang="scss">
$h: 32px;
$border-color: #d9d9d9;
$color: #333;
$blue: #40a9ff;
$radius: 4px;
.gulu-button {
    box-sizing: border-box;
    height: $h;
    padding: 0 12px;
    cursor: pointer;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    white-space: nowrap;
    background: white;
    color: $color;
    border: 1px solid $border-color;
    border-radius: $radius;
    box-shadow: 0 1px 0 fade-out(black, 0.95);
    & + & {
        margin-left: 8px;
    }
    &:hover,
    &:focus {
        color: $blue;
        border-color: $blue;
    }
    &:focus {
        outline: none;
    }
    &::-moz-focus-inner {
        border: 0;
    }
    &.gulu-theme-link{
        border-color: transparent;
        box-shadow: none;
        color: $blue;
        &:hover,&:focus{
            color: lighten($blue, 10%);
        }
    }
    &.gulu-theme-text{
        border-color: transparent;
        box-shadow: none;
        color: inherit;
        &:hover,&:focus{
            background: darken(white, 5%);;
        }
    }
    &.gulu-size-big {
        font-size: 24px;
        height: 48px;
        padding: 0 16px;
    }
    &.gulu-size-small {
        font-size: 12px;
        height: 20px;
        padding: 0 4px;
    }
}  
</style>
