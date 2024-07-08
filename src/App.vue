<!-- src/App.vue -->
<template>
  <div class="container">
    <h1>CV Generator</h1>
    <TemplateSelector
      v-if="!selectedTemplate"
      :templates="templates"
      @select="handleTemplateSelect"
    />
    <CVEditor v-if="selectedTemplate" :template="selectedTemplate" />
  </div>
</template>

<script>
import TemplateSelector from './components/TemplateSelector.vue';
import CVEditor from './components/CVEditor.vue';

export default {
  components: {
    TemplateSelector,
    CVEditor
  },
  data() {
    return {
      templates: [],
      selectedTemplate: null
    };
  },
  created() {
    fetch('./templates/templates.json')
      .then(response => response.json())
      .then(data => {
        this.templates = data;
      });
  },
  methods: {
    handleTemplateSelect(template) {
      this.selectedTemplate = template;
    }
  }
};
</script>

<style>
.container {
  width: 80%;
  margin: 0 auto;
}
</style>
