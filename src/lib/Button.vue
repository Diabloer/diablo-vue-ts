<template>
<button class="blo-button" :class="classes"  :disabled="disabled">
    <span v-if="loading" class="blo-loadingIndicator"></span>
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
    /* vue 属性继承 */
    // 1. 默认属性传给跟元素
    // 2. inheritAttrs: false 可以禁用默认属性传给跟元素
    // 3. v-bind="$attrs"/ content.attrs 绑定属性传递位置
    props: {
        theme: {
            type: String,
            default: "button"
        },
        size: {
            type: String,
            default: "normal"
        },
        level: {
            type: String,
            default: "normal"
        },
        disabled: {
            type: Boolean,
            default: false
        },
        loading: {
            type: Boolean,
            default: false
        }
    },
    setup(props, context) {
        const { theme, size, level } = props;
        const classes = computed(() => {
            return {
                [`blo-theme-${theme}`]: theme,
                [`blo-size-${size}`]: size,
                [`blo-level-${level}`]: level
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
$blue: #409EFF;
$radius: 4px;
$red: #F56C6C;
$grey: grey;
.blo-button {
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
    transition: background 250ms;
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
    &.blo-theme-link{
        border-color: transparent;
        box-shadow: none;
        color: $blue;
        &:hover,&:focus{
            color: lighten($blue, 10%);
        }
    }
    &.blo-theme-text{
        border-color: transparent;
        box-shadow: none;
        color: inherit;
        &:hover,&:focus{
            background: darken(white, 5%);;
        }
    }
    &.blo-size-big {
        font-size: 24px;
        height: 48px;
        padding: 0 16px;
    }
    &.blo-size-small {
        font-size: 12px;
        height: 20px;
        padding: 0 4px;
    }
    &.blo-theme-button {
        &.blo-level-main {
            background: $blue;
            color: white;
            border-color: $blue;
            &:hover,
            &:focus {
                background: darken($blue, 10%);
                border-color: darken($blue, 10%);
            }
        }
        &.blo-level-danger {
            background: $red;
            border-color: $red;
            color: white;
            &:hover,
            &:focus {
                background: darken($red, 10%);
                border-color: darken($red, 10%);
            }
        }
    }
    &.blo-theme-link {
        &.blo-level-danger {
            color: $red;
            &:hover,
            &:focus {
                color: darken($red, 10%);
            }
        }
    }
    &.blo-theme-text {
        &.blo-level-main {
            color: $blue;
            &:hover,
            &:focus {
                color: darken($blue, 10%);
            }
        }
        &.blo-level-danger {
            color: $red;
            &:hover,
            &:focus {
                color: darken($red, 10%);
            }
        }
    }
    &.blo-theme-button {
        &[disabled] {
            cursor: not-allowed;
            color: $grey;
            &:hover {
                border-color: $grey;
            }
        }
    }
    &.blo-theme-link, &.blo-theme-text {
        &[disabled] {
            cursor: not-allowed;
            color: $grey;
        }
    }
    > .blo-loadingIndicator{
        width: 14px;
        height: 14px;
        display: inline-block;
        margin-right: 4px;
        border-radius: 8px; 
        border-color: $blue $blue $blue transparent;
        border-style: solid;
        border-width: 2px;
        animation: blo-spin 1s infinite linear;
    }
}
@keyframes blo-spin {
    0%{transform: rotate(0deg)} 
    100%{transform: rotate(360deg)} 
}  
</style>
