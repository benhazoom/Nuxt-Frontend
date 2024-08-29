<template>
    <div class="container">
        <h2>This page demonstrates using a state to render my items, and also not using the default layout</h2>
        <MyItem 
            v-for="rental in myRentals"
            :key="rental.id"
            :item="rental"
        />
    </div>
</template>

<script>
import { mapState } from 'vuex';

    export default {
        layout: "no-nav",
        computed: {
            ...mapState([
                'myRentals'
            ])
        }
    }
</script>

<style scoped>
    .container {
        padding: 5rem 0
    }
</style>