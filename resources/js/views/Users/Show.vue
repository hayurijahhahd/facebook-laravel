<template>
    <div>

    </div>
</template>

<script>
    export default {
        name: "Show",

        data: () => {
            return {
                user: null,
                loading: true
            }
        },

        mounted() {
            axios.get('/api/users/' + this.$route.params.userId)
                .then(res => {
                    this.user = res.data;
                })
                .catch(error => {
                    console.log('Unable to fetch the user from the server.');
                })
                .finally(() => {
                    this.loading = false;
                });
        }
    }
</script>

<style scoped>

</style>
