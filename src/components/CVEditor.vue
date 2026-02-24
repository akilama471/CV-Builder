<template>
  <div class="cv-editor">
    <header class="editor-header">
      <button class="btn-secondary" @click="goBack">← Change Template</button>
      <h2>Edit Your CV</h2>
      <div class="header-actions">
        <button class="btn-secondary" @click="resetData">Reset</button>
        <button class="btn-primary" @click="exportPDF">Download PDF</button>
      </div>
    </header>

    <div class="editor-content">
      <div class="editor-form">
        <div class="form-section">
          <h3 @click="toggleSection('personal')" class="section-toggle">
            Personal Information <span>{{ openSections.personal ? '▼' : '▶' }}</span>
          </h3>
          <div v-show="openSections.personal" class="section-content">
            <div class="form-group">
              <label>Profile Photo</label>
              <div class="image-upload">
                <div v-if="cvData.personal.image" class="image-preview">
                  <img :src="cvData.personal.image" alt="Profile" />
                  <button class="remove-image" @click="cvData.personal.image = ''">✕</button>
                </div>
                <label v-else class="upload-label">
                  <input type="file" accept="image/*" @change="handleImageUpload" hidden />
                  <span>+ Upload Photo</span>
                </label>
              </div>
            </div>
            <div class="form-group">
              <label>Full Name</label>
              <input v-model="cvData.personal.fullName" type="text" placeholder="John Doe" />
            </div>
            <div class="form-row">
              <div class="form-group">
                <label>Email</label>
                <input v-model="cvData.personal.email" type="email" placeholder="john@email.com" />
              </div>
              <div class="form-group">
                <label>Phone</label>
                <input v-model="cvData.personal.phone" type="tel" placeholder="+1 234 567 890" />
              </div>
            </div>
            <div class="form-group">
              <label>Address</label>
              <input v-model="cvData.personal.address" type="text" placeholder="City, Country" />
            </div>
            <div class="form-row">
              <div class="form-group">
                <label>LinkedIn</label>
                <input v-model="cvData.personal.linkedin" type="text" placeholder="linkedin.com/in/..." />
              </div>
              <div class="form-group">
                <label>Website</label>
                <input v-model="cvData.personal.website" type="text" placeholder="johndoe.com" />
              </div>
            </div>
            <div class="form-group">
              <label>Professional Summary</label>
              <textarea v-model="cvData.personal.summary" rows="4" placeholder="Brief summary of your professional background..."></textarea>
            </div>
          </div>
        </div>

        <div class="form-section">
          <h3 @click="toggleSection('experience')" class="section-toggle">
            Work Experience <span>{{ openSections.experience ? '▼' : '▶' }}</span>
          </h3>
          <div v-show="openSections.experience" class="section-content">
            <div v-for="(exp, index) in cvData.experience" :key="exp.id" class="item-card">
              <div class="item-header">
                <span>Experience {{ index + 1 }}</span>
                <button class="btn-icon" @click="removeItem('experience', index)">✕</button>
              </div>
              <div class="form-group">
                <label>Company</label>
                <input v-model="exp.company" type="text" placeholder="Company Name" />
              </div>
              <div class="form-group">
                <label>Position</label>
                <input v-model="exp.position" type="text" placeholder="Job Title" />
              </div>
              <div class="form-row">
                <div class="form-group">
                  <label>Start Date</label>
                  <input v-model="exp.startDate" type="text" placeholder="2020-01" />
                </div>
                <div class="form-group">
                  <label>End Date</label>
                  <input v-model="exp.endDate" type="text" placeholder="Present" />
                </div>
              </div>
              <div class="form-group">
                <label>Description</label>
                <textarea v-model="exp.description" rows="3" placeholder="Key responsibilities and achievements..."></textarea>
              </div>
            </div>
            <button class="btn-add" @click="addItem('experience')">+ Add Experience</button>
          </div>
        </div>

        <div class="form-section">
          <h3 @click="toggleSection('education')" class="section-toggle">
            Education <span>{{ openSections.education ? '▼' : '▶' }}</span>
          </h3>
          <div v-show="openSections.education" class="section-content">
            <div v-for="(edu, index) in cvData.education" :key="edu.id" class="item-card">
              <div class="item-header">
                <span>Education {{ index + 1 }}</span>
                <button class="btn-icon" @click="removeItem('education', index)">✕</button>
              </div>
              <div class="form-group">
                <label>Institution</label>
                <input v-model="edu.institution" type="text" placeholder="University Name" />
              </div>
              <div class="form-row">
                <div class="form-group">
                  <label>Degree</label>
                  <input v-model="edu.degree" type="text" placeholder="Bachelor's Degree" />
                </div>
                <div class="form-group">
                  <label>Field of Study</label>
                  <input v-model="edu.field" type="text" placeholder="Computer Science" />
                </div>
              </div>
              <div class="form-row">
                <div class="form-group">
                  <label>Start Date</label>
                  <input v-model="edu.startDate" type="text" placeholder="2016-09" />
                </div>
                <div class="form-group">
                  <label>End Date</label>
                  <input v-model="edu.endDate" type="text" placeholder="2020-05" />
                </div>
              </div>
            </div>
            <button class="btn-add" @click="addItem('education')">+ Add Education</button>
          </div>
        </div>

        <div class="form-section">
          <h3 @click="toggleSection('skills')" class="section-toggle">
            Skills <span>{{ openSections.skills ? '▼' : '▶' }}</span>
          </h3>
          <div v-show="openSections.skills" class="section-content">
            <div v-for="(skill, index) in cvData.skills" :key="skill.id" class="skill-item">
              <input v-model="skill.name" type="text" placeholder="Skill name" class="skill-input" />
              <input v-model="skill.level" type="text" placeholder="Level" class="level-input" />
              <button class="btn-icon" @click="removeItem('skills', index)">✕</button>
            </div>
            <button class="btn-add" @click="addItem('skills')">+ Add Skill</button>
          </div>
        </div>

        <div class="form-section">
          <h3 @click="toggleSection('projects')" class="section-toggle">
            Projects <span>{{ openSections.projects ? '▼' : '▶' }}</span>
          </h3>
          <div v-show="openSections.projects" class="section-content">
            <div v-for="(project, index) in cvData.projects" :key="project.id" class="item-card">
              <div class="item-header">
                <span>Project {{ index + 1 }}</span>
                <button class="btn-icon" @click="removeItem('projects', index)">✕</button>
              </div>
              <div class="form-group">
                <label>Project Name</label>
                <input v-model="project.name" type="text" placeholder="Project Name" />
              </div>
              <div class="form-group">
                <label>Description</label>
                <textarea v-model="project.description" rows="2" placeholder="Project description..."></textarea>
              </div>
              <div class="form-group">
                <label>Technologies Used</label>
                <input v-model="project.technologies" type="text" placeholder="Vue.js, Node.js, MongoDB" />
              </div>
              <div class="form-group">
                <label>Link</label>
                <input v-model="project.link" type="text" placeholder="github.com/project" />
              </div>
            </div>
            <button class="btn-add" @click="addItem('projects')">+ Add Project</button>
          </div>
        </div>

        <div class="form-section">
          <h3 @click="toggleSection('certifications')" class="section-toggle">
            Certifications <span>{{ openSections.certifications ? '▼' : '▶' }}</span>
          </h3>
          <div v-show="openSections.certifications" class="section-content">
            <div v-for="(cert, index) in cvData.certifications" :key="cert.id" class="item-card">
              <div class="item-header">
                <span>Certification {{ index + 1 }}</span>
                <button class="btn-icon" @click="removeItem('certifications', index)">✕</button>
              </div>
              <div class="form-group">
                <label>Certification Name</label>
                <input v-model="cert.name" type="text" placeholder="AWS Solutions Architect" />
              </div>
              <div class="form-group">
                <label>Issuing Organization</label>
                <input v-model="cert.issuer" type="text" placeholder="Amazon Web Services" />
              </div>
              <div class="form-group">
                <label>Date</label>
                <input v-model="cert.date" type="text" placeholder="2023-01" />
              </div>
            </div>
            <button class="btn-add" @click="addItem('certifications')">+ Add Certification</button>
          </div>
        </div>

        <div class="form-section">
          <h3 @click="toggleSection('languages')" class="section-toggle">
            Languages <span>{{ openSections.languages ? '▼' : '▶' }}</span>
          </h3>
          <div v-show="openSections.languages" class="section-content">
            <div v-for="(lang, index) in cvData.languages" :key="lang.id" class="skill-item">
              <input v-model="lang.name" type="text" placeholder="Language" class="skill-input" />
              <input v-model="lang.level" type="text" placeholder="Proficiency" class="level-input" />
              <button class="btn-icon" @click="removeItem('languages', index)">✕</button>
            </div>
            <button class="btn-add" @click="addItem('languages')">+ Add Language</button>
          </div>
        </div>

        <div class="form-section">
          <h3 @click="toggleSection('exams')" class="section-toggle">
            Exams <span>{{ openSections.exams ? '▼' : '▶' }}</span>
          </h3>
          <div v-show="openSections.exams" class="section-content">
            <div v-for="(exam, examIndex) in cvData.exams" :key="exam.id" class="item-card">
              <div class="item-header">
                <span>Exam {{ examIndex + 1 }}</span>
                <button class="btn-icon" @click="removeItem('exams', examIndex)">✕</button>
              </div>
              <div class="form-row">
                <div class="form-group">
                  <label>Exam Name</label>
                  <input v-model="exam.name" type="text" placeholder="e.g., SSC, HSC, A-Level" />
                </div>
                <div class="form-group">
                  <label>Year</label>
                  <input v-model="exam.year" type="text" placeholder="e.g., 2018" />
                </div>
                <div class="form-group">
                  <label>Place/Board</label>
                  <input v-model="exam.place" type="text" placeholder="e.g., Dhaka Board" />
                </div>
              </div>
              <div class="subjects-section">
                <label>Subjects & Marks</label>
                <div v-for="(subject, subIndex) in exam.subjects" :key="subIndex" class="subject-row">
                  <input v-model="subject.name" type="text" placeholder="Subject" class="subject-input" />
                  <input v-model="subject.marks" type="text" placeholder="Marks" class="marks-input" />
                  <button class="btn-icon" @click="exam.subjects.splice(subIndex, 1)">✕</button>
                </div>
                <button class="btn-add-subject" @click="exam.subjects.push({ name: '', marks: '' })">+ Add Subject</button>
              </div>
            </div>
            <button class="btn-add" @click="addItem('exams')">+ Add Exam</button>
          </div>
        </div>

        <div class="form-section">
          <h3 @click="toggleSection('interests')" class="section-toggle">
            Interests <span>{{ openSections.interests ? '▼' : '▶' }}</span>
          </h3>
          <div v-show="openSections.interests" class="section-content">
            <div class="form-group">
              <label>Interests & Hobbies</label>
              <textarea v-model="cvData.interests" rows="2" placeholder="Technology, Reading, Hiking..."></textarea>
            </div>
          </div>
        </div>
      </div>

      <div class="editor-preview">
        <div class="preview-header">
          <h3>Live Preview</h3>
          <span class="template-name">{{ template.name }}</span>
        </div>
        <div class="preview-container">
          <div id="cv-preview" class="cv-preview" :class="'template-' + template.id">
            <component :is="previewComponent" :data="cvData" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import html2pdf from 'html2pdf.js';
import ClassicTemplate from './templates/ClassicTemplate.vue';
import ModernTemplate from './templates/ModernTemplate.vue';
import MinimalTemplate from './templates/MinimalTemplate.vue';
import CreativeTemplate from './templates/CreativeTemplate.vue';
import Template1 from './templates/Template1.vue';
import Template2 from './templates/Template2.vue';
import Template3 from './templates/Template3.vue';
import Template4 from './templates/Template4.vue';
import Template5 from './templates/Template5.vue';

const STORAGE_KEY = 'cv-builder-data';

export default {
  name: 'CVEditor',
  components: {
    ClassicTemplate,
    ModernTemplate,
    MinimalTemplate,
    CreativeTemplate,
    Template1,
    Template2,
    Template3,
    Template4,
    Template5
  },
  props: {
    template: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      cvData: JSON.parse(JSON.stringify(this.template.defaultData)),
      openSections: {
        personal: true,
        experience: true,
        education: true,
        skills: true,
        projects: false,
        certifications: false,
        languages: false,
        exams: false,
        interests: false
      },
      templateComponents: {
        classic: 'ClassicTemplate',
        modern: 'ModernTemplate',
        minimal: 'MinimalTemplate',
        creative: 'CreativeTemplate',
        template1: 'Template1',
        template2: 'Template2',
        template3: 'Template3',
        template4: 'Template4',
        template5: 'Template5'
      }
    };
  },
  computed: {
    previewComponent() {
      return this.templateComponents[this.template.id] || 'ClassicTemplate';
    }
  },
  watch: {
    cvData: {
      handler() {
        this.saveToStorage();
      },
      deep: true
    }
  },
  created() {
    this.loadFromStorage();
  },
  methods: {
    toggleSection(section) {
      this.openSections[section] = !this.openSections[section];
    },
    handleImageUpload(event) {
      const file = event.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
          this.cvData.personal.image = e.target.result;
        };
        reader.readAsDataURL(file);
      }
    },
    addItem(section) {
      const newItem = this.getDefaultItem(section);
      this.cvData[section].push(newItem);
    },
    removeItem(section, index) {
      this.cvData[section].splice(index, 1);
    },
    getDefaultItem(section) {
      const defaults = {
        experience: { id: Date.now(), company: '', position: '', startDate: '', endDate: '', description: '' },
        education: { id: Date.now(), institution: '', degree: '', field: '', startDate: '', endDate: '' },
        skills: { id: Date.now(), name: '', level: '' },
        projects: { id: Date.now(), name: '', description: '', technologies: '', link: '' },
        certifications: { id: Date.now(), name: '', issuer: '', date: '' },
        languages: { id: Date.now(), name: '', level: '' },
        exams: { id: Date.now(), name: '', year: '', place: '', subjects: [{ name: '', marks: '' }] }
      };
      return defaults[section];
    },
    saveToStorage() {
      const data = {
        templateId: this.template.id,
        cvData: this.cvData,
        savedAt: new Date().toISOString()
      };
      localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
    },
    loadFromStorage() {
      const saved = localStorage.getItem(STORAGE_KEY);
      if (saved) {
        try {
          const parsed = JSON.parse(saved);
          if (parsed.templateId === this.template.id) {
            this.cvData = parsed.cvData;
            if (!this.cvData.exams) {
              this.cvData.exams = [];
            }
          }
        } catch (e) {
          console.error('Failed to load saved data:', e);
        }
      }
    },
    resetData() {
      if (confirm('Reset all data to default? This cannot be undone.')) {
        this.cvData = JSON.parse(JSON.stringify(this.template.defaultData));
        localStorage.removeItem(STORAGE_KEY);
      }
    },
    exportPDF() {
      const element = document.getElementById('cv-preview');
      const opt = {
        margin: 0,
        filename: `${this.cvData.personal.fullName.replace(/\s+/g, '_')}_CV.pdf`,
        image: { type: 'jpeg', quality: 0.98 },
        html2canvas: { scale: 2, useCORS: true },
        jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' },
        pagebreak: { mode: ['avoid-all', 'css', 'legacy'] }
      };
      html2pdf().set(opt).from(element).save();
    },
    goBack() {
      this.$emit('back');
    }
  }
};
</script>

<style scoped>
.cv-editor {
  display: flex;
  flex-direction: column;
  height: calc(100vh - 40px);
}

.editor-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 24px;
  background: #fff;
  border-bottom: 1px solid #e0e0e0;
}

.editor-header h2 {
  margin: 0;
  font-size: 1.5rem;
}

.header-actions {
  display: flex;
  gap: 12px;
}

.editor-content {
  display: flex;
  flex: 1;
  overflow: hidden;
}

.editor-form {
  width: 50%;
  padding: 24px;
  overflow-y: auto;
  background: #f5f5f5;
}

.editor-preview {
  width: 50%;
  display: flex;
  flex-direction: column;
  background: #e0e0e0;
}

.preview-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 24px;
  background: #fff;
  border-bottom: 1px solid #e0e0e0;
}

.preview-header h3 {
  margin: 0;
}

.template-name {
  font-size: 0.875rem;
  color: #666;
  background: #f0f0f0;
  padding: 4px 12px;
  border-radius: 4px;
}

.preview-container {
  flex: 1;
  padding: 24px;
  overflow-y: auto;
  display: flex;
  justify-content: center;
}

.cv-preview {
  width: 210mm;
  min-height: 297mm;
  background: #fff;
  box-shadow: 0 4px 20px rgba(0,0,0,0.15);
  transform-origin: top center;
}

.form-section {
  background: #fff;
  border-radius: 8px;
  margin-bottom: 16px;
  overflow: hidden;
}

.section-toggle {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 20px;
  margin: 0;
  cursor: pointer;
  background: #fff;
  font-size: 1rem;
  font-weight: 600;
  transition: background 0.2s;
}

.section-toggle:hover {
  background: #f8f8f8;
}

.section-toggle span {
  font-size: 0.75rem;
  color: #666;
}

.section-content {
  padding: 0 20px 20px;
}

.form-group {
  margin-bottom: 16px;
}

.form-group label {
  display: block;
  margin-bottom: 6px;
  font-size: 0.875rem;
  font-weight: 500;
  color: #333;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 10px 12px;
  border: 1px solid #ddd;
  border-radius: 6px;
  font-size: 0.9rem;
  transition: border-color 0.2s;
  box-sizing: border-box;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #4a90d9;
}

.form-row {
  display: flex;
  gap: 16px;
}

.form-row .form-group {
  flex: 1;
}

.image-upload {
  display: flex;
  align-items: center;
  gap: 16px;
}

.image-preview {
  position: relative;
  width: 80px;
  height: 80px;
}

.image-preview img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 8px;
  border: 2px solid #ddd;
}

.remove-image {
  position: absolute;
  top: -8px;
  right: -8px;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  background: #d32f2f;
  color: #fff;
  border: none;
  cursor: pointer;
  font-size: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.upload-label {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 80px;
  height: 80px;
  border: 2px dashed #ccc;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s;
}

.upload-label:hover {
  border-color: #4a90d9;
  background: #f8f8f8;
}

.upload-label span {
  font-size: 0.8rem;
  color: #666;
}

.item-card {
  background: #f9f9f9;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 16px;
  margin-bottom: 12px;
}

.item-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 12px;
  font-weight: 600;
  color: #333;
}

.btn-icon {
  background: none;
  border: none;
  color: #999;
  cursor: pointer;
  font-size: 1rem;
  padding: 4px 8px;
}

.btn-icon:hover {
  color: #d32f2f;
}

.skill-item {
  display: flex;
  gap: 8px;
  margin-bottom: 8px;
  align-items: center;
}

.skill-item .skill-input {
  flex: 2;
}

.skill-item .level-input {
  flex: 1;
}

.btn-add {
  width: 100%;
  padding: 12px;
  background: #f0f0f0;
  border: 2px dashed #ccc;
  border-radius: 6px;
  cursor: pointer;
  font-size: 0.9rem;
  color: #666;
  transition: all 0.2s;
}

.btn-add:hover {
  background: #e8e8e8;
  border-color: #999;
}

.subjects-section {
  margin-top: 16px;
  padding-top: 16px;
  border-top: 1px solid #eee;
}

.subjects-section label {
  display: block;
  margin-bottom: 8px;
  font-size: 0.875rem;
  font-weight: 500;
  color: #333;
}

.subject-row {
  display: flex;
  gap: 8px;
  margin-bottom: 8px;
  align-items: center;
}

.subject-row .subject-input {
  flex: 3;
}

.subject-row .marks-input {
  flex: 1;
}

.btn-add-subject {
  padding: 8px 12px;
  background: #f0f0f0;
  border: 1px dashed #ccc;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.8rem;
  color: #666;
  width: 100%;
}

.btn-add-subject:hover {
  background: #e8e8e8;
}

.btn-primary {
  padding: 10px 20px;
  background: #4a90d9;
  color: #fff;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 0.9rem;
  font-weight: 500;
  transition: background 0.2s;
}

.btn-primary:hover {
  background: #3a7bc8;
}

.btn-secondary {
  padding: 10px 20px;
  background: #fff;
  color: #333;
  border: 1px solid #ddd;
  border-radius: 6px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: all 0.2s;
}

.btn-secondary:hover {
  background: #f5f5f5;
}

@media (max-width: 1024px) {
  .editor-content {
    flex-direction: column;
  }
  
  .editor-form,
  .editor-preview {
    width: 100%;
  }
  
  .editor-preview {
    height: 500px;
  }
}
</style>
