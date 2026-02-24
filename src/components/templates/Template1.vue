<template>
  <div class="cv-template template1">
    <header class="cv-header">
      <div class="header-left">
        <h1>{{ data.personal.fullName }}</h1>
        <div class="contact-row">
          <span v-if="data.personal.phone">{{ data.personal.phone }}</span>
          <span v-if="data.personal.email">{{ data.personal.email }}</span>
          <span v-if="data.personal.address">{{ data.personal.address }}</span>
        </div>
        <div class="contact-row">
          <span v-if="data.personal.linkedin">{{ data.personal.linkedin }}</span>
          <span v-if="data.personal.website">{{ data.personal.website }}</span>
        </div>
      </div>
    </header>

    <div class="cv-body">
      <div class="main-content">
        <section v-if="data.personal.summary" class="cv-section">
          <h2>Profile</h2>
          <p>{{ data.personal.summary }}</p>
        </section>

        <section v-if="data.experience.length" class="cv-section">
          <h2>Employment History</h2>
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
      </div>

      <div class="sidebar">
        <section v-if="data.skills.length" class="sidebar-section">
          <h3>Core Skills</h3>
          <div v-for="skill in data.skills" :key="skill.id" class="skill-item">
            <span>{{ skill.name }}</span>
            <span v-if="skill.level" class="skill-level">{{ skill.level }}</span>
          </div>
        </section>

        <section v-if="data.languages.length" class="sidebar-section">
          <h3>Languages</h3>
          <div v-for="lang in data.languages" :key="lang.id" class="language-item">
            <span class="lang-name">{{ lang.name }}</span>
            <span class="lang-level">{{ lang.level }}</span>
          </div>
        </section>

        <section v-if="data.interests" class="sidebar-section">
          <h3>Interests</h3>
          <p class="interests">{{ data.interests }}</p>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProfessionalTemplate',
  props: {
    data: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
.cv-template {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 10pt;
  line-height: 1.5;
  color: #333;
  width: 210mm;
  min-height: 297mm;
  background: #fff;
  box-sizing: border-box;
}

.cv-header {
  padding: 30px 40px;
  border-bottom: 1px solid #ddd;
}

.header-left h1 {
  margin: 0 0 8px;
  font-size: 24pt;
  font-weight: 600;
  color: #1a1a1a;
}

.contact-row {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  font-size: 9pt;
  color: #555;
  margin-top: 4px;
}

.cv-body {
  display: flex;
}

.main-content {
  flex: 1;
  padding: 30px 40px;
  border-right: 1px solid #eee;
}

.sidebar {
  width: 220px;
  padding: 30px 20px;
  background: #fafafa;
}

.cv-section {
  margin-bottom: 24px;
  page-break-inside: avoid;
}

.cv-section:last-child {
  page-break-after: auto;
}

.cv-section h2 {
  font-size: 11pt;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin: 0 0 16px;
  color: #333;
  border-bottom: 1px solid #ccc;
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
  color: #555;
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
  color: #0066cc;
}

.subjects-list {
  font-size: 9pt;
  color: #555;
  margin-top: 4px;
}

.sidebar-section {
  margin-bottom: 24px;
}

.sidebar-section h3 {
  font-size: 10pt;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin: 0 0 12px;
  color: #333;
  border-bottom: 1px solid #ccc;
  padding-bottom: 4px;
}

.skill-item {
  display: flex;
  justify-content: space-between;
  font-size: 9pt;
  padding: 4px 0;
  border-bottom: 1px solid #eee;
}

.skill-level {
  color: #666;
}

.language-item {
  display: flex;
  justify-content: space-between;
  font-size: 9pt;
  padding: 4px 0;
  border-bottom: 1px solid #eee;
}

.lang-name {
  font-weight: 500;
}

.lang-level {
  color: #666;
}

.interests {
  font-size: 9pt;
  color: #555;
  line-height: 1.4;
}
</style>
