<!-- src/components/CVEditor.vue -->
<template>
  <div>
    <h2>Edit Your CV</h2>
    <form @submit.prevent="saveCV">
      <div v-for="(field, key) in cvData" :key="key">
        <label :for="key">{{ key }}:</label>
        <input v-model="cvData[key]" :id="key" />
      </div>
      <button type="submit">Download PDF</button>
    </form>
    <div id="cv-content" v-html="renderedTemplate"></div>
  </div>
</template>

<script>
import html2pdf from 'html2pdf.js';
import mustache from 'mustache';

export default {
  props: ['template'],
  data() {
    return {
      cvData: { ...this.template.defaultData }
    };
  },
  computed: {
    renderedTemplate() {
      return mustache.render(this.template.templateHtml, this.cvData);
    }
  },
  methods: {
    saveCV() {
      const element = document.getElementById('cv-content');
      html2pdf().from(element).save();
    }
  }
};
</script>

<style>
#cv-content {
  border: 1px solid #ccc;
  padding: 20px;
  margin-top: 20px;
}
</style>
