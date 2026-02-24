<template>
  <div class="cv-template modern">
    <div class="cv-sidebar">
      <div class="sidebar-content">
        <div v-if="data.personal.image" class="profile-image">
          <img :src="data.personal.image" alt="Profile" />
        </div>
        <h1>{{ data.personal.fullName }}</h1>
        
        <div class="contact-section">
          <h3>Contact</h3>
          <div v-if="data.personal.email" class="contact-item">{{ data.personal.email }}</div>
          <div v-if="data.personal.phone" class="contact-item">{{ data.personal.phone }}</div>
          <div v-if="data.personal.address" class="contact-item">{{ data.personal.address }}</div>
          <div v-if="data.personal.linkedin" class="contact-item">{{ data.personal.linkedin }}</div>
          <div v-if="data.personal.website" class="contact-item">{{ data.personal.website }}</div>
        </div>

        <div v-if="data.skills.length" class="sidebar-section">
          <h3>Skills</h3>
          <div v-for="skill in data.skills" :key="skill.id" class="skill-item">
            <div class="skill-name">{{ skill.name }}</div>
            <div class="skill-level">{{ skill.level }}</div>
          </div>
        </div>

        <div v-if="data.languages.length" class="sidebar-section">
          <h3>Languages</h3>
          <div v-for="lang in data.languages" :key="lang.id" class="language-item">
            <span>{{ lang.name }}</span>
            <span class="lang-level">{{ lang.level }}</span>
          </div>
        </div>

        <div v-if="data.exams && data.exams.length" class="sidebar-section">
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
        </div>

        <div v-if="data.interests" class="sidebar-section">
          <h3>Interests</h3>
          <p class="interests-text">{{ data.interests }}</p>
        </div>
      </div>
    </div>

    <div class="cv-main">
      <section v-if="data.personal.summary" class="cv-section">
        <h2>Profile</h2>
        <p>{{ data.personal.summary }}</p>
      </section>

      <section v-if="data.experience.length" class="cv-section">
        <h2>Work Experience</h2>
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
          <div>{{ edu.degree }} in {{ edu.field }}</div>
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
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModernTemplate',
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
  display: flex;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 10pt;
  line-height: 1.5;
  min-height: 297mm;
  width: 210mm;
  background: #fff;
  box-sizing: border-box;
}

.cv-sidebar {
  width: 200px;
  background: #2c3e50;
  color: #fff;
  padding: 40px 20px;
  flex-shrink: 0;
}

.sidebar-content h1 {
  font-size: 18pt;
  margin: 0 0 30px;
  line-height: 1.2;
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
  border: 3px solid rgba(255,255,255,0.3);
}

.contact-section,
.sidebar-section {
  margin-bottom: 30px;
}

.contact-section h3,
.sidebar-section h3 {
  font-size: 11pt;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin: 0 0 12px;
  opacity: 0.8;
}

.contact-item {
  font-size: 9pt;
  margin-bottom: 6px;
  word-break: break-word;
}

.skill-item {
  margin-bottom: 10px;
}

.skill-name {
  font-weight: 500;
}

.skill-level {
  font-size: 9pt;
  opacity: 0.8;
}

.language-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 6px;
}

.exam-item {
  margin-bottom: 10px;
}

.exam-block {
  margin-bottom: 16px;
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
  font-size: 9pt;
  opacity: 0.7;
  margin-bottom: 4px;
}

.exam-subjects {
  margin-top: 4px;
}

.subject-entry {
  display: flex;
  justify-content: space-between;
  font-size: 9pt;
  padding: 2px 0;
}

.exam-score {
  font-size: 9pt;
  opacity: 0.8;
}

.lang-level {
  opacity: 0.8;
}

.interests-text {
  font-size: 9pt;
  opacity: 0.8;
}

.cv-main {
  flex: 1;
  padding: 40px;
}

.cv-section {
  margin-bottom: 28px;
  page-break-inside: avoid;
}

.cv-section h2 {
  font-size: 14pt;
  color: #2c3e50;
  border-bottom: 2px solid #2c3e50;
  padding-bottom: 8px;
  margin: 0 0 20px;
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
  color: #2c3e50;
}

.date {
  font-size: 9pt;
  color: #666;
}

.company {
  font-weight: 500;
  color: #555;
  margin-bottom: 8px;
}

.experience-item,
.education-item,
.project-item,
.cert-item {
  margin-bottom: 18px;
}

.technologies {
  font-size: 9pt;
  color: #666;
  margin-top: 4px;
}

.link {
  font-size: 9pt;
  color: #3498db;
}
</style>
