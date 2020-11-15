<template>
<div :size="size">
    <button v-bind="rest">
        <slot />
    </button>
</div>
</template>

<script lang="ts">
export default {
    inheritAttrs: false,
    // 1. props 需要先声明才能取值，attrs 不用申明
    // 2. props 不包含事件，attrs 包含
    // 3. props 没有申明属性，会跑到 attrs 中
    // 4. props 支持 string 以外的类型，attrs 只有 string 类型
    props: {
        size: String,
        disabled: Boolean
    },
    setup(props, context) {
        const {size, ...rest} = context.attrs;
        return {size, rest}
    }
}
</script>

<style lang="scss" scoped>
    
</style>
