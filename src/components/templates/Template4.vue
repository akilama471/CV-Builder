<template>
  <div class="cv-template template4">
    <div class="cv-sidebar">
      <div v-if="data.personal.image" class="profile-image">
        <img :src="data.personal.image" alt="Profile" />
      </div>
      <h1>{{ data.personal.fullName }}</h1>
      
      <div class="sidebar-section">
        <h3>Contact</h3>
        <div v-if="data.personal.phone" class="contact-item">{{ data.personal.phone }}</div>
        <div v-if="data.personal.email" class="contact-item">{{ data.personal.email }}</div>
        <div v-if="data.personal.address" class="contact-item">{{ data.personal.address }}</div>
        <div v-if="data.personal.linkedin" class="contact-item">{{ data.personal.linkedin }}</div>
        <div v-if="data.personal.website" class="contact-item">{{ data.personal.website }}</div>
      </div>

      <div v-if="data.skills.length" class="sidebar-section">
        <h3>Skills</h3>
        <div v-for="skill in data.skills" :key="skill.id" class="skill-item">
          <span class="skill-name">{{ skill.name }}</span>
          <div class="skill-bar">
            <div class="skill-fill" :style="{ width: getSkillWidth(skill.level) }"></div>
          </div>
        </div>
      </div>

      <div v-if="data.languages.length" class="sidebar-section">
        <h3>Languages</h3>
        <div v-for="lang in data.languages" :key="lang.id" class="language-item">
          <span>{{ lang.name }}</span>
          <span class="lang-level">{{ lang.level }}</span>
        </div>
      </div>

      <div v-if="data.interests" class="sidebar-section">
        <h3>Interests</h3>
        <p class="interests">{{ data.interests }}</p>
      </div>
    </div>

    <div class="cv-main">
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
  </div>
</template>

<script>
export default {
  name: 'ModernDarkTemplate',
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
  display: flex;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: 10pt;
  line-height: 1.5;
  color: #333;
  min-height: 297mm;
  background: #fff;
  width: 210mm;
  box-sizing: border-box;
}

.cv-sidebar {
  width: 180px;
  background: #2c3e50;
  color: #fff;
  padding: 30px 15px;
  flex-shrink: 0;
}

.profile-image {
  width: 80px;
  height: 80px;
  margin: 0 auto 20px;
}

.profile-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
  border: 3px solid rgba(255,255,255,0.3);
}

.cv-sidebar h1 {
  font-size: 14pt;
  margin: 0 0 25px;
  text-align: center;
  line-height: 1.3;
}

.sidebar-section {
  margin-bottom: 25px;
}

.sidebar-section h3 {
  font-size: 9pt;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin: 0 0 12px;
  opacity: 0.7;
  border-bottom: 1px solid rgba(255,255,255,0.2);
  padding-bottom: 4px;
}

.contact-item {
  font-size: 8pt;
  margin-bottom: 6px;
  word-break: break-word;
  opacity: 0.9;
}

.skill-item {
  margin-bottom: 10px;
}

.skill-name {
  display: block;
  font-size: 8pt;
  margin-bottom: 2px;
}

.skill-bar {
  height: 4px;
  background: rgba(255,255,255,0.2);
  border-radius: 2px;
  overflow: hidden;
}

.skill-fill {
  height: 100%;
  background: #3498db;
  border-radius: 2px;
}

.language-item {
  display: flex;
  justify-content: space-between;
  font-size: 8pt;
  margin-bottom: 6px;
  opacity: 0.9;
}

.lang-level {
  opacity: 0.7;
}

.interests {
  font-size: 8pt;
  opacity: 0.9;
  line-height: 1.4;
}

.cv-main {
  flex: 1;
  padding: 30px 30px;
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
  color: #2c3e50;
  border-bottom: 2px solid #2c3e50;
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
  color: #2c3e50;
}

.date {
  font-size: 9pt;
  color: #666;
}

.company {
  font-weight: 500;
  color: #3498db;
  margin-bottom: 6px;
  font-size: 9pt;
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
  color: #3498db;
}

.subjects-list {
  font-size: 9pt;
  color: #555;
  margin-top: 4px;
}
</style>
