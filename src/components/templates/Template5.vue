<template>
  <div class="cv-template template5">
    <div class="cv-sidebar">
      <div v-if="data.personal.image" class="profile-image">
        <img :src="data.personal.image" alt="Profile" />
      </div>
      <div v-else class="profile-placeholder"></div>

      <div class="sidebar-section">
        <h3>Contact</h3>
        <div v-if="data.personal.phone" class="contact-item">
          <span class="icon">&#9742;</span> {{ data.personal.phone }}
        </div>
        <div v-if="data.personal.email" class="contact-item">
          <span class="icon">&#9993;</span> {{ data.personal.email }}
        </div>
        <div v-if="data.personal.address" class="contact-item">
          <span class="icon">&#9906;</span> {{ data.personal.address }}
        </div>
        <div v-if="data.personal.linkedin" class="contact-item">
          <span class="icon">&#9679;</span> {{ data.personal.linkedin }}
        </div>
        <div v-if="data.personal.website" class="contact-item">
          <span class="icon">&#9679;</span> {{ data.personal.website }}
        </div>
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
          <span class="lang-name">{{ lang.name }}</span>
          <span class="lang-level">{{ lang.level }}</span>
        </div>
      </div>

      <div v-if="data.interests" class="sidebar-section">
        <h3>Interests</h3>
        <p class="interests">{{ data.interests }}</p>
      </div>
    </div>

    <div class="cv-main">
      <header class="cv-header">
        <h1>{{ data.personal.fullName }}</h1>
      </header>

      <section v-if="data.personal.summary" class="cv-section">
        <h2>Profile</h2>
        <p>{{ data.personal.summary }}</p>
      </section>

      <section v-if="data.education.length" class="cv-section">
        <h2>Education</h2>
        <div v-for="edu in data.education" :key="edu.id" class="education-item">
          <div class="item-header">
            <h3>{{ edu.institution }}</h3>
            <span class="date">{{ edu.startDate }} - {{ edu.endDate }}</span>
          </div>
          <div class="degree">{{ edu.degree }} {{ edu.field ? 'in ' + edu.field : '' }}</div>
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
  name: 'ElegantTemplate',
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
  width: 210mm;
  min-height: 297mm;
  background: #fff;
  box-sizing: border-box;
}

.cv-sidebar {
  width: 180px;
  background: #f8f9fa;
  padding: 30px 15px;
  flex-shrink: 0;
}

.profile-image {
  width: 100px;
  height: 100px;
  margin: 0 auto 20px;
}

.profile-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 4px;
  border: 2px solid #ddd;
}

.profile-placeholder {
  width: 100px;
  height: 100px;
  margin: 0 auto 20px;
  background: #e0e0e0;
  border-radius: 4px;
}

.sidebar-section {
  margin-bottom: 24px;
}

.sidebar-section h3 {
  font-size: 9pt;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin: 0 0 12px;
  color: #2c7a7b;
  border-bottom: 1px solid #ddd;
  padding-bottom: 4px;
}

.contact-item {
  font-size: 8pt;
  margin-bottom: 8px;
  display: flex;
  align-items: flex-start;
  gap: 6px;
  word-break: break-word;
}

.contact-item .icon {
  color: #2c7a7b;
  font-size: 8pt;
}

.skill-item {
  margin-bottom: 10px;
}

.skill-name {
  display: block;
  font-size: 8pt;
  margin-bottom: 3px;
}

.skill-bar {
  height: 6px;
  background: #e0e0e0;
  border-radius: 3px;
  overflow: hidden;
}

.skill-fill {
  height: 100%;
  background: #2c7a7b;
  border-radius: 3px;
}

.language-item {
  display: flex;
  justify-content: space-between;
  font-size: 8pt;
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
  font-size: 8pt;
  color: #555;
  line-height: 1.4;
}

.cv-main {
  flex: 1;
  padding: 30px 25px;
}

.cv-header {
  margin-bottom: 20px;
  padding-bottom: 15px;
  border-bottom: 2px solid #2c7a7b;
}

.cv-header h1 {
  margin: 0;
  font-size: 22pt;
  font-weight: 600;
  color: #2c7a7b;
  letter-spacing: 0.5px;
}

.cv-section {
  margin-bottom: 20px;
  page-break-inside: avoid;
}

.cv-section h2 {
  font-size: 11pt;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin: 0 0 14px;
  color: #333;
  border-bottom: 1px solid #ddd;
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
  color: #333;
}

.date {
  font-size: 9pt;
  color: #666;
}

.degree {
  font-size: 9pt;
  color: #555;
}

.company {
  font-size: 9pt;
  color: #2c7a7b;
  font-weight: 500;
  margin-bottom: 4px;
}

.experience-item,
.education-item,
.project-item,
.cert-item,
.exam-item {
  margin-bottom: 14px;
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
  color: #2c7a7b;
}

.subjects-list {
  font-size: 9pt;
  color: #555;
  margin-top: 2px;
}
</style>
