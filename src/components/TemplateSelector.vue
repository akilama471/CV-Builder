<!-- src/components/TemplateSelector.vue -->
<template>
    <div>
        <h2>Select a Template</h2>
        <div class="templates">
            <div v-for="template in templates" :key="template.id" class="template">
                <img :src="template.thumbnail" @click="selectTemplate(template)" />
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['templates'],
    methods: {
        selectTemplate(template) {
            this.$emit('select', template);
        }
    }
};
</script>

<style>
.templates {
    display: flex;
    flex-wrap: wrap;
}
.template {
    margin: 10px;
    cursor: pointer;
}
</style>
