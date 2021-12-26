<template>
    <div>
        <ul>
            <li>
                <!-- #8 -->
                <nuxt-link to="/nav/about">About</nuxt-link>
                <nuxt-link to="/nav/contact">Contact</nuxt-link>
            </li>
        </ul>
        <div class="bg-gray-500">
            <!-- #8 -->
            <nuxt-child />
        </div>
    </div>
</template>

<script>
    export default {
        
    } 
</script>

<style lang="scss" scoped>

</style>