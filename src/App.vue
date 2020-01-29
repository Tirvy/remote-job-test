<template>
    <div id="app">
        <block-posts :posts="posts_list" @getComments="getComments"></block-posts>
        <block-filter
                :body.sync="filter.full"
                :name.sync="filter.name"
        ></block-filter>
    </div>
</template>

<script>
  import axios from "axios";

  import BlockFilter from "./components/block-filter";
  import BlockPosts from "./components/block-posts";

  export default {
        name: "app",
        components: {BlockFilter, BlockPosts},
        data() {
            return {
                users: [],
                posts: [],
                comments: {},
                filter: {
                    name: "",
                    full: ""
                }
            };
        },
        created() {
            this.getPosts();
            this.getUsers();
        },
        computed: {
            users_hashed() {
                let ret = {};
                this.users.forEach(user => {
                    ret[user.id] = user;
                });
                return ret;
            },
            posts_mapped() {
                if (this.posts.length && this.users.length) {
                    return this.posts.map(item => {
                        return {
                            ...item,
                            user: this.users_hashed[item.userId],
                            comments: this.comments[item.id]
                        };
                    });
                }
                return [];
            },
            posts_filtered() {
                return this.posts_mapped.filter(item => {
                    return (this.contains(item.title, this.filter.name) || this.contains(item.user.name, this.filter.name)) && (this.contains(item.body, this.filter.full))
                });
            },
            posts_list() {
                return this.posts_filtered;
            }
        },
        methods: {
            contains(where, what) {
                return !where || !what || where.toUpperCase().includes(what.toUpperCase());
            },
            getComments(post_id) {
                axios.get(`https://jsonplaceholder.typicode.com/comments`, {
                    params: {
                        postId: post_id
                    }
                }).then(res => {
                    this.$set(this.comments, post_id, res.data);
                });
            },
            getPosts() {
                axios.get("https://jsonplaceholder.typicode.com/posts").then(res => {
                    this.posts = res.data;
                });
            },
            getUsers() {
                axios.get("https://jsonplaceholder.typicode.com/users").then(res => {
                    this.users = res.data;
                });
            }
        }
    };
</script>

<style lang="scss">
    #app {
        font-size: 14px;
        display: flex;
        justify-content: center;
        flex-direction: row;
        flex-wrap: wrap-reverse;
    }

    .bg-blue {
        background: #e6f5ff;
        border: solid #d6e5ef;
        border-width: 0;
    }

    .input-header {
        padding-left: 4px;
    }
</style>
