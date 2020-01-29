<template>
    <div class="posts-block">
        <post-item
                :key="post.id"
                :value="post"
                @getComments="$emit('getComments', post.id)"
                v-for="post in posts"
        ></post-item>
    </div>
</template>

<script>
  import PostItem from "./post";

  export default {
        name: "PostsBlock",
        components: {PostItem},
        directives: {},
        mixins: [],
        props: ["posts"],
        data() {
            return {};
        },
        computed: {},
        methods: {}
    };
</script>

<style scoped>
    .posts-block {
        max-width: 800px;
        width: 800px;
    }
</style>
