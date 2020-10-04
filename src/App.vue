<template>
<router-view />
</template>

<script lang="ts">
import {
    ref,
    provide
} from 'vue'
export default {
    name: 'App',
    setup() {
        const widthPage = document.documentElement.clientWidth;
        const asideVisible = ref(widthPage <= 500 ? false : true)
        provide('asideVisible', asideVisible)
    }
}
</script>
