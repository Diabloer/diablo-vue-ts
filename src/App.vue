<template>
<router-view />
</template>

<script lang="ts">
import {
    ref,
    provide
} from 'vue'
import {
    router
} from './router'
export default {
    name: 'App',
    setup() {
        const widthPage = document.documentElement.clientWidth;
        const asideVisible = ref(widthPage <= 500 ? false : true)
        provide('asideVisible', asideVisible)
        router.afterEach((to, from) => {
            if (widthPage <= 500) asideVisible.value = false;
        })
    }
}
</script>
