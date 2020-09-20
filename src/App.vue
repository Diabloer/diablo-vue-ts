<template>
<div>导航栏 ｜ <router-link to="/">Frank</router-link>
    <router-link to="/frank2">Frank2</router-link>
</div>
<router-view />
</template>

<script>
export default {
    name: 'App'
}
</script>
