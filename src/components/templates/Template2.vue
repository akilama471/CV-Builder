<template>
  <div class="cv-template template2">
    <header class="cv-header">
      <h1>{{ data.personal.fullName }}</h1>
      <div class="header-info">
        <span v-if="data.personal.phone" class="info-item">
          <span class="icon">&#9742;</span> {{ data.personal.phone }}
        </span>
        <span v-if="data.personal.email" class="info-item">
          <span class="icon">&#9993;</span> {{ data.personal.email }}
        </span>
        <span v-if="data.personal.address" class="info-item">
          <span class="icon">&#9906;</span> {{ data.personal.address }}
        </span>
        <span v-if="data.personal.linkedin" class="info-item">
          <span class="icon">&#9679;</span> {{ data.personal.linkedin }}
        </span>
        <span v-if="data.personal.website" class="info-item">
          <span class="icon">&#9679;</span> {{ data.personal.website }}
        </span>
      </div>
    </header>

    <div class="cv-content">
      <section v-if="data.personal.summary" class="cv-section">
        <h2>Profile</h2>
        <p>{{ data.personal.summary }}</p>
      </section>

      <section v-if="data.experience.length" class="cv-section">
        <h2>Experience</h2>
        <div v-for="exp in data.experience" :key="exp.id" class="experience-item">
          <div class="item-header">
            <h3>{{ exp.position }}</h3>
            <span class="date">{{ exp.startDate }} - {{ exp.endDate }}</span>
          </div>
          <div class="company">{{ exp.company }}</div>
          <p>{{ exp.description }}</p>
        </div>
      </section>

      <section v-if="data.education.length" class="cv-section">
        <h2>Education</h2>
        <div v-for="edu in data.education" :key="edu.id" class="education-item">
          <div class="item-header">
            <h3>{{ edu.institution }}</h3>
            <span class="date">{{ edu.startDate }} - {{ edu.endDate }}</span>
          </div>
          <div>{{ edu.degree }} {{ edu.field ? 'in ' + edu.field : '' }}</div>
        </div>
      </section>

      <section v-if="data.skills.length" class="cv-section">
        <h2>Skills</h2>
        <div class="skills-grid">
          <div v-for="skill in data.skills" :key="skill.id" class="skill-item">
            <span class="skill-name">{{ skill.name }}</span>
            <div class="skill-bar">
              <div class="skill-fill" :style="{ width: getSkillWidth(skill.level) }"></div>
            </div>
          </div>
        </div>
      </section>

      <section v-if="data.projects.length" class="cv-section">
        <h2>Projects</h2>
        <div v-for="project in data.projects" :key="project.id" class="project-item">
          <div class="item-header">
            <h3>{{ project.name }}</h3>
            <span v-if="project.link" class="link">{{ project.link }}</span>
          </div>
          <p>{{ project.description }}</p>
          <div v-if="project.technologies" class="technologies">{{ project.technologies }}</div>
        </div>
      </section>

      <section v-if="data.certifications.length" class="cv-section">
        <h2>Certifications</h2>
        <div v-for="cert in data.certifications" :key="cert.id" class="cert-item">
          <div class="item-header">
            <h3>{{ cert.name }}</h3>
            <span class="date">{{ cert.date }}</span>
          </div>
          <div>{{ cert.issuer }}</div>
        </div>
      </section>

      <section v-if="data.languages.length" class="cv-section">
        <h2>Languages</h2>
        <div class="languages-list">
          <span v-for="lang in data.languages" :key="lang.id" class="language-tag">
            {{ lang.name }} - {{ lang.level }}
          </span>
        </div>
      </section>

      <section v-if="data.exams && data.exams.length" class="cv-section">
        <h2>Examinations</h2>
        <div v-for="exam in data.exams" :key="exam.id" class="exam-item">
          <div class="item-header">
            <h3>{{ exam.name }}</h3>
            <span class="date">{{ exam.year }} {{ exam.place ? '- ' + exam.place : '' }}</span>
          </div>
          <div class="subjects-list">
            <span v-for="(subject, index) in exam.subjects" :key="index">
              {{ subject.name }}: {{ subject.marks }}<span v-if="index < exam.subjects.length - 1">, </span>
            </span>
          </div>
        </div>
      </section>

      <section v-if="data.interests" class="cv-section">
        <h2>Interests</h2>
        <p>{{ data.interests }}</p>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ExecutiveTemplate',
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  methods: {
    getSkillWidth(level) {
      const levels = {
        'Beginner': '25%',
        'Elementary': '40%',
        'Intermediate': '55%',
        'Advanced': '70%',
        'Native': '100%',
        'Fluent': '85%'
      };
      return levels[level] || '60%';
    }
  }
};
</script>

<style scoped>
.cv-template {
  font-family: 'Arial', sans-serif;
  font-size: 10pt;
  line-height: 1.5;
  color: #333;
  width: 210mm;
  min-height: 297mm;
  background: #fff;
  box-sizing: border-box;
}

.cv-header {
  background: #1e4d7b;
  color: #fff;
  padding: 30px 40px;
}

.cv-header h1 {
  margin: 0 0 12px;
  font-size: 26pt;
  font-weight: 400;
}

.header-info {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  font-size: 9pt;
}

.info-item {
  display: flex;
  align-items: center;
  gap: 4px;
}

.icon {
  font-size: 10pt;
}

.cv-content {
  padding: 30px 40px;
}

.cv-section {
  margin-bottom: 24px;
  page-break-inside: avoid;
}

.cv-section h2 {
  font-size: 12pt;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin: 0 0 16px;
  color: #1e4d7b;
  border-bottom: 2px solid #1e4d7b;
  padding-bottom: 6px;
}

.item-header {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  margin-bottom: 2px;
}

.item-header h3 {
  margin: 0;
  font-size: 11pt;
  font-weight: 600;
}

.date {
  font-size: 9pt;
  color: #666;
}

.company {
  font-size: 9pt;
  color: #1e4d7b;
  font-weight: 500;
  margin-bottom: 6px;
}

.experience-item,
.education-item,
.project-item,
.cert-item,
.exam-item {
  margin-bottom: 16px;
}

.experience-item p,
.project-item p {
  margin: 6px 0 0;
  color: #444;
  font-size: 9pt;
}

.technologies {
  font-size: 9pt;
  color: #666;
  margin-top: 4px;
}

.link {
  font-size: 9pt;
  color: #1e4d7b;
}

.subjects-list {
  font-size: 9pt;
  color: #555;
  margin-top: 4px;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 12px;
}

.skill-item {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.skill-name {
  font-size: 9pt;
  font-weight: 500;
}

.skill-bar {
  height: 8px;
  background: #e0e0e0;
  border-radius: 4px;
  overflow: hidden;
}

.skill-fill {
  height: 100%;
  background: #1e4d7b;
  border-radius: 4px;
}

.languages-list {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.language-tag {
  background: #f0f0f0;
  padding: 4px 12px;
  border-radius: 4px;
  font-size: 9pt;
}
</style>
