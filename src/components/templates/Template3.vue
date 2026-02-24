<template>
  <div class="cv-template template3">
    <header class="cv-header">
      <h1>{{ data.personal.fullName }}</h1>
      <div class="contact-info">
        <span v-if="data.personal.phone">{{ data.personal.phone }}</span>
        <span v-if="data.personal.email">{{ data.personal.email }}</span>
        <span v-if="data.personal.address">{{ data.personal.address }}</span>
        <span v-if="data.personal.linkedin">{{ data.personal.linkedin }}</span>
        <span v-if="data.personal.website">{{ data.personal.website }}</span>
      </div>
    </header>

    <div class="cv-content">
      <section v-if="data.personal.summary" class="cv-section">
        <h2>Profile</h2>
        <p>{{ data.personal.summary }}</p>
      </section>

      <section v-if="data.skills.length" class="cv-section">
        <h2>Skills</h2>
        <div class="skills-list">
          <div v-for="skill in data.skills" :key="skill.id" class="skill-item">
            <span class="skill-name">{{ skill.name }}</span>
            <div class="skill-bar">
              <div class="skill-fill" :style="{ width: getSkillWidth(skill.level) }"></div>
            </div>
          </div>
        </div>
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
  name: 'MinimalistTemplate',
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
        'Advanced': '75%',
        'Expert': '90%',
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
  font-family: 'Calibri', Arial, sans-serif;
  font-size: 10pt;
  line-height: 1.4;
  color: #222;
  width: 210mm;
  min-height: 297mm;
  background: #fff;
  box-sizing: border-box;
}

.cv-header {
  padding: 30px 40px;
  border-bottom: 2px solid #333;
  margin-bottom: 20px;
}

.cv-header h1 {
  margin: 0 0 8px;
  font-size: 28pt;
  font-weight: 400;
  letter-spacing: 1px;
}

.contact-info {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  font-size: 9pt;
  color: #555;
}

.cv-content {
  padding: 0 40px 30px;
}

.cv-section {
  margin-bottom: 20px;
  page-break-inside: avoid;
}

.cv-section h2 {
  font-size: 11pt;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin: 0 0 12px;
  color: #333;
  border-bottom: 1px solid #ccc;
  padding-bottom: 4px;
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
  color: #444;
  font-weight: 500;
  margin-bottom: 4px;
}

.experience-item,
.education-item,
.project-item,
.cert-item,
.exam-item {
  margin-bottom: 12px;
}

.experience-item p,
.project-item p {
  margin: 4px 0 0;
  color: #444;
  font-size: 9pt;
}

.technologies {
  font-size: 9pt;
  color: #666;
  margin-top: 2px;
}

.link {
  font-size: 9pt;
  color: #0066cc;
}

.subjects-list {
  font-size: 9pt;
  color: #555;
  margin-top: 2px;
}

.skills-list {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 10px;
}

.skill-item {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.skill-name {
  font-size: 9pt;
  font-weight: 500;
}

.skill-bar {
  height: 6px;
  background: #ddd;
  border-radius: 3px;
  overflow: hidden;
}

.skill-fill {
  height: 100%;
  background: #333;
  border-radius: 3px;
}
</style>
