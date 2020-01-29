<template>
    <div class="block-filter">
        <div class="filters" style="">
            <div style="font-size: 16px;">
                Фильтры
            </div>
            <div style="margin: 8px 0;">
                <div class="input-header">Имя/название</div>
                <input :value="name" @input="$emit('update:name', $event.target.value)">
            </div>
            <div>
                <div class="input-header">Контент</div>
                <input :value="body" @input="$emit('update:body', $event.target.value)">
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'BlockDescription',
        components: {},
        directives: {},
        mixins: [],
        props: ['name', 'body'],
        data() {
            return {}
        },
        computed: {},
        methods: {}
    }
</script>

<style scoped>
    .block-filter {
        background: #ccc;
        padding: 16px;
    }

    .filters {
        position: sticky;
        top: 0;
        min-width: 250px;
    }
</style>