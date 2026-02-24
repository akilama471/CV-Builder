<template>
  <div class="cv-template creative">
    <div class="cv-header">
      <div class="header-accent"></div>
      <div v-if="data.personal.image" class="profile-image">
        <img :src="data.personal.image" alt="Profile" />
      </div>
      <h1>{{ data.personal.fullName }}</h1>
      <div class="contact-info">
        <span v-if="data.personal.email">✉ {{ data.personal.email }}</span>
        <span v-if="data.personal.phone">☎ {{ data.personal.phone }}</span>
        <span v-if="data.personal.address">⌖ {{ data.personal.address }}</span>
        <span v-if="data.personal.linkedin">◈ {{ data.personal.linkedin }}</span>
        <span v-if="data.personal.website">🌐 {{ data.personal.website }}</span>
      </div>
    </div>

    <div class="cv-body">
      <div class="main-content">
        <section v-if="data.personal.summary" class="cv-section">
          <h2><span class="section-icon">◆</span> About Me</h2>
          <p>{{ data.personal.summary }}</p>
        </section>

        <section v-if="data.experience.length" class="cv-section">
          <h2><span class="section-icon">◆</span> Work Experience</h2>
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
          <h2><span class="section-icon">◆</span> Education</h2>
          <div v-for="edu in data.education" :key="edu.id" class="education-item">
            <div class="item-header">
              <h3>{{ edu.institution }}</h3>
              <span class="date">{{ edu.startDate }} - {{ edu.endDate }}</span>
            </div>
            <div>{{ edu.degree }} in {{ edu.field }}</div>
          </div>
        </section>

        <section v-if="data.projects.length" class="cv-section">
          <h2><span class="section-icon">◆</span> Projects</h2>
          <div v-for="project in data.projects" :key="project.id" class="project-item">
            <div class="item-header">
              <h3>{{ project.name }}</h3>
              <span v-if="project.link" class="link">{{ project.link }}</span>
            </div>
            <p>{{ project.description }}</p>
            <div v-if="project.technologies" class="tech-tags">
              <span v-for="tech in project.technologies.split(',')" :key="tech" class="tech-tag">{{ tech.trim() }}</span>
            </div>
          </div>
        </section>

        <section v-if="data.certifications.length" class="cv-section">
          <h2><span class="section-icon">◆</span> Certifications</h2>
          <div v-for="cert in data.certifications" :key="cert.id" class="cert-item">
            <div class="item-header">
              <h3>{{ cert.name }}</h3>
              <span class="date">{{ cert.date }}</span>
            </div>
            <div>{{ cert.issuer }}</div>
          </div>
        </section>
      </div>

      <div class="sidebar">
        <section v-if="data.skills.length" class="sidebar-section">
          <h3>Skills</h3>
          <div v-for="skill in data.skills" :key="skill.id" class="skill-bar">
            <div class="skill-info">
              <span>{{ skill.name }}</span>
              <span>{{ skill.level }}</span>
            </div>
          </div>
        </section>

        <section v-if="data.languages.length" class="sidebar-section">
          <h3>Languages</h3>
          <div v-for="lang in data.languages" :key="lang.id" class="language-item">
            <span class="lang-name">{{ lang.name }}</span>
            <span class="lang-level">{{ lang.level }}</span>
          </div>
        </section>

        <section v-if="data.exams && data.exams.length" class="sidebar-section">
          <h3>Examinations</h3>
          <div v-for="exam in data.exams" :key="exam.id" class="exam-block">
            <div class="exam-header">
              <span class="exam-name">{{ exam.name }}</span>
              <span class="exam-year">{{ exam.year }}</span>
            </div>
            <div v-if="exam.place" class="exam-place">{{ exam.place }}</div>
            <div class="exam-subjects">
              <div v-for="(subject, index) in exam.subjects" :key="index" class="subject-entry">
                <span>{{ subject.name }}</span>
                <span>{{ subject.marks }}</span>
              </div>
            </div>
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
  name: 'CreativeTemplate',
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
  font-family: 'Roboto', 'Open Sans', sans-serif;
  font-size: 10pt;
  line-height: 1.5;
  color: #333;
  width: 210mm;
  min-height: 297mm;
  background: #fff;
  box-sizing: border-box;
}

.cv-header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: #fff;
  padding: 40px;
}

.header-accent {
  width: 60px;
  height: 4px;
  background: #fff;
  margin-bottom: 20px;
}

.profile-image {
  width: 100px;
  height: 100px;
  margin-bottom: 20px;
}

.profile-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
  border: 4px solid rgba(255,255,255,0.5);
}

.cv-header h1 {
  font-size: 28pt;
  margin: 0 0 16px;
  font-weight: 300;
}

.contact-info {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  font-size: 9pt;
}

.contact-info span {
  white-space: nowrap;
}

.cv-body {
  display: flex;
  padding: 30px 40px;
}

.main-content {
  flex: 1;
  padding-right: 30px;
}

.sidebar {
  width: 220px;
  padding: 20px;
  background: #f8f9fa;
}

.cv-section {
  margin-bottom: 28px;
  page-break-inside: avoid;
}

.cv-section h2 {
  font-size: 14pt;
  margin: 0 0 16px;
  color: #667eea;
  display: flex;
  align-items: center;
  gap: 8px;
}

.section-icon {
  font-size: 10pt;
}

.item-header {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  margin-bottom: 4px;
}

.item-header h3 {
  margin: 0;
  font-size: 12pt;
  color: #333;
}

.date {
  font-size: 9pt;
  color: #888;
}

.company {
  font-weight: 500;
  color: #667eea;
  margin-bottom: 8px;
}

.experience-item,
.education-item,
.project-item,
.cert-item {
  margin-bottom: 18px;
}

.project-item p,
.experience-item p {
  margin: 6px 0 0;
  color: #555;
}

.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-top: 8px;
}

.tech-tag {
  background: #667eea;
  color: #fff;
  padding: 2px 8px;
  border-radius: 3px;
  font-size: 8pt;
}

.link {
  font-size: 9pt;
  color: #667eea;
}

.sidebar-section {
  margin-bottom: 24px;
}

.sidebar-section h3 {
  font-size: 11pt;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin: 0 0 12px;
  color: #667eea;
}

.skill-bar {
  margin-bottom: 10px;
}

.skill-info {
  display: flex;
  justify-content: space-between;
  font-size: 9pt;
}

.language-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
  font-size: 9pt;
}

.exam-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 8px;
  font-size: 9pt;
}

.exam-block {
  margin-bottom: 14px;
}

.exam-header {
  display: flex;
  justify-content: space-between;
  font-weight: 500;
}

.exam-year {
  opacity: 0.8;
}

.exam-place {
  font-size: 8pt;
  opacity: 0.7;
}

.exam-subjects {
  margin-top: 4px;
}

.subject-entry {
  display: flex;
  justify-content: space-between;
  font-size: 8pt;
  padding: 1px 0;
  opacity: 0.9;
}

.exam-name {
  font-weight: 500;
}

.exam-score {
  color: #666;
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
}
</style>
