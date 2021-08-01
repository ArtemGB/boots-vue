<template>
    <div>
        <NavMenu/>
        <router-view class="mt-1"/>
    </div>
</template>

<script>
import NavMenu from './NavMenu.vue'

export default {
    name: 'Layout',
    components: {
        NavMenu
    }
}
</script>