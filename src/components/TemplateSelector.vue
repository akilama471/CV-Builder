<template>
  <div class="template-selector">
    <div class="selector-header">
      <h2>Choose a Template</h2>
      <p>Select a resume template to get started</p>
    </div>
    <div class="templates-grid">
      <div 
        v-for="template in templates" 
        :key="template.id" 
        class="template-card"
        @click="selectTemplate(template)"
      >
        <div class="template-preview">
          <div class="template-preview-inner" :class="'preview-' + template.id">
            <div class="preview-header"></div>
            <div class="preview-content">
              <div class="preview-line short"></div>
              <div class="preview-line"></div>
              <div class="preview-line"></div>
              <div class="preview-line medium"></div>
            </div>
          </div>
        </div>
        <div class="template-info">
          <h3>{{ template.name }}</h3>
          <span class="use-btn">Use Template</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TemplateSelector',
  props: {
    templates: {
      type: Array,
      required: true
    }
  },
  methods: {
    selectTemplate(template) {
      this.$emit('select', template);
    }
  }
};
</script>

<style scoped>
.template-selector {
  padding: 40px 20px;
}

.selector-header {
  text-align: center;
  margin-bottom: 40px;
}

.selector-header h2 {
  font-size: 2rem;
  margin: 0 0 10px;
  color: #333;
}

.selector-header p {
  color: #666;
  margin: 0;
}

.templates-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 24px;
  max-width: 1200px;
  margin: 0 auto;
}

.template-card {
  background: #fff;
  border-radius: 12px;
  overflow: hidden;
  cursor: pointer;
  transition: all 0.3s;
  border: 2px solid transparent;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}

.template-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.12);
  border-color: #4a90d9;
}

.template-preview {
  aspect-ratio: 1 / 1.4;
  background: #f5f5f5;
  padding: 16px;
}

.template-preview-inner {
  background: #fff;
  height: 100%;
  border-radius: 4px;
  overflow: hidden;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.preview-classic .preview-header {
  background: #333;
  height: 20%;
}

.preview-modern .preview-header {
  background: #2c3e50;
  width: 30%;
  height: 100%;
  float: left;
}

.preview-modern .preview-content {
  margin-left: 30%;
}

.preview-minimal .preview-header {
  background: #222;
  height: 15%;
}

.preview-minimal .preview-content {
  padding: 10px;
}

.preview-creative .preview-header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  height: 25%;
}

.preview-content {
  padding: 10px;
}

.preview-line {
  background: #ddd;
  height: 6px;
  border-radius: 3px;
  margin-bottom: 6px;
}

.preview-line.short {
  width: 40%;
}

.preview-line.medium {
  width: 70%;
}

.template-info {
  padding: 16px;
  text-align: center;
}

.template-info h3 {
  margin: 0 0 8px;
  font-size: 1.1rem;
  color: #333;
}

.use-btn {
  display: inline-block;
  padding: 6px 16px;
  background: #f0f0f0;
  border-radius: 4px;
  font-size: 0.85rem;
  color: #666;
  transition: all 0.2s;
}

.template-card:hover .use-btn {
  background: #4a90d9;
  color: #fff;
}
</style>
