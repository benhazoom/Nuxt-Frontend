<template>
    <div>
        <h3>Customer Reviews</h3>
        <div v-if="!$fetchState.pending">
            <div v-if="reviewers.results">
                <ReviewCard
                v-for="reviewer in reviewers.results"
                :key="reviewer.login.uuid"
                :review="reviewer"
                />
            </div>
        </div>
        <div v-else>
            <h2>...Loading/loader component</h2>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                reviewers: []
            }
        },
        async fetch() {
            this.reviewers = await fetch('https://randomuser.me/api/?results=5').then((res) => res.json())
        }
    }
</script>

<style lang="scss" scoped>

</style>

<!-- data fetching
with asyncData is happening only in the pages and not inside components
with fetch allow us to provide a loader  -->
