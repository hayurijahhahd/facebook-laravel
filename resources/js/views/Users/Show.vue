<template>
    <div class="flex flex-col items-center">
        <div class="relative mb-8">
            <div class="w-100 h-64 overflow-hidden z-10">
                <img alt="user background image" class="object-cover w-full"
                     src="https://pbs.twimg.com/media/EAkcgKLU4AIjYP7?format=jpg&name=large">
            </div>

            <div class="absolute flex items-center bottom-0 left-0 -mb-8 ml-12 z-20">
                <div class="w-32">
                    <img alt="user profile image"
                         class="object-cover w-32 h-32 border-4 border-gray-200 rounded-full shadow-lg"
                         src="https://pbs.twimg.com/media/EL8XDZfVAAACOwV?format=jpg&name=large">
                </div>
                <p class="ml-4 text-2xl text-gray-100">{{ user.data.attributes.name }}</p>
            </div>
        </div>

        <p v-if="postLoading">Loading post...</p>
        <Post :key="post.data.post_id" :post="post" v-else v-for="post in posts.data"/>

        <p v-if=" ! postLoading && posts.data.length < 1">Create a new Post</p>
    </div>
</template>

<script>
    import Post from "../../components/Post";

    export default {
        name: "Show",

        components: {
            Post
        },

        data: () => {
            return {
                user: [],
                posts: [],
                userLoading: true,
                postLoading: true
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
                    this.userLoading = false;
                });

            axios.get('/api/users/' + this.$route.params.userId + '/posts')
                .then(res => {
                    this.posts = res.data;
                })
                .catch(error => {
                    console.log('Unable to fetch posts');
                })
                .finally(() => {
                    this.postLoading = false;
                });
        }
    }
</script>

<style scoped>

</style>
