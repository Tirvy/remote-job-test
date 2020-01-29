<template>
    <div class="post-item">
        <div class="post-content bg-blue">
            <div class="post-main">
                <div style="display: flex; justify-content: flex-start">
                    <img height="100" src="https://placekitten.com/100/100" style="margin-right: 8px" width="100"/>
                    <div>
                        <div class="user narrow-screen">
                            {{ value.user.name }}
                        </div>
                        <div class="title narrow-screen">
                            {{ value.title }}
                        </div>
                    </div>
                </div>
                <div>
                    <div class="user wide-screen">
                        {{ value.user.name }}
                    </div>
                    <div class="title wide-screen">
                        {{ value.title }}
                    </div>
                    <div class="content">
                        {{ value.body }}
                    </div>
                </div>
            </div>
            <div class="comment-expander-container">
                <div
                        @click="openComments"
                        class="comment-expander"
                        v-if="!comments_open"
                >
                    Открыть комментарии
                </div>
                <div @click="closeComments" v-else-if="!value.comments">
                    загрузка
                </div>
            </div>
        </div>
        <comment-section
                :value="value.comments"
                @hideComments="closeComments"
                v-if="comments_open && value.comments"
        ></comment-section>
    </div>
</template>

<script>
  import CommentSection from "./comment-section";

  export default {
        name: "Index",
        components: {CommentSection},
        directives: {},
        mixins: [],
        props: ["value"],
        data() {
            return {
                comments_open: false
            };
        },
        computed: {},
        methods: {
            openComments() {
                if (!this.value.comments) {
                    this.$emit("getComments");
                }
                this.comments_open = !this.comments_open;
            },
            closeComments() {
                this.comments_open = false;
            }
        }
    };
</script>

<style scoped>
    .post-item {
        margin: 16px 16px;
    }

    .post-main {
        display: flex;
        justify-content: flex-start
    }

    .post-content {
        padding: 8px 16px;
        border-width: 1px;
    }

    .user {
        color: #999;
        font-size: 12px;
    }

    .title {
        font-size: 17px;
        padding-top: 4px;
    }

    .content {
        padding-top: 4px;
    }

    .comment-expander-container {
        display: flex;
        justify-content: flex-end;
        height: 20px;
        margin-top: 4px;
    }

    .comment-expander {
        color: dodgerblue;
        cursor: pointer;
    }

    @media (min-width: 600px) {
        .narrow-screen {
            display: none;
        }
    }

    @media (max-width: 600px) {
        .post-main {
            flex-direction: column;
            align-items: flex-start;
        }

        .wide-screen {
            display: none;
        }
    }
</style>
