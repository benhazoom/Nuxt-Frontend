<template>
    <div>
        <div class="container">
            <NuxtLink to="/">Go Back</NuxtLink>
        </div>
        <Nuxt />
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style scoped>
    .container {
        padding-top: 6rem;
        margin-bottom: -5rem;
    }
</style>
<!-- we can use this layout in a page by specifing it in the script tag in  'export default' like in my-items  -->