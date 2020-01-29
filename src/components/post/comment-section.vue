<template>
    <div class="comment-section">
        <div class="comment-container bg-blue" v-for="comment in value">
            <div style="display: flex;justify-content: flex-start">
                <img height="60" src="https://placekitten.com/40/60" style="flex-shrink: 0;" width="40">
                <div style="margin-left: 8px;">
                    <div class="name">
                        {{ comment.name }} <span style="color: grey; font-size: 13px">промурчал</span>
                    </div>
                    <div class="content">
                        {{ comment.body }}
                    </div>
                </div>
            </div>
        </div>
        <div class="controls">

            <div @click="$emit('hideComments')" class="button comments-closer bg-blue">
                Скрыть комментарии
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "CommentSection",
        components: {},
        directives: {},
        mixins: [],
        props: ["value"],
        data() {
            return {
                editing: null
            };
        },
        computed: {},
        methods: {}
    };
</script>

<style scoped>
    .comment-section {
        margin: 0 30px 50px 30px;
        position: relative;
    }

    .comment-container {
        border-width: 0 1px 1px 1px;
        padding: 8px 16px;
    }

    .name {
        font-size: 17px;
        margin-bottom: 4px;
    }

    .controls {
        display: flex;
        justify-content: flex-end;
    }

    .button {
        margin-left: 20px;
        color: dodgerblue;
        cursor: pointer;
        padding: 4px 8px;
    }

    .comments-adder {
    }

    .comments-closer {
    }
</style>
