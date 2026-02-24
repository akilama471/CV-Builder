<template>
  <div class="cv-template minimal">
    <header class="cv-header">
      <div v-if="data.personal.image" class="profile-image">
        <img :src="data.personal.image" alt="Profile" />
      </div>
      <div class="header-text">
        <h1>{{ data.personal.fullName }}</h1>
        <div class="contact-info">
        <template v-if="data.personal.email">
          <span>{{ data.personal.email }}</span>
          <span class="separator">·</span>
        </template>
        <template v-if="data.personal.phone">
          <span>{{ data.personal.phone }}</span>
          <span class="separator">·</span>
        </template>
        <template v-if="data.personal.address">
          <span>{{ data.personal.address }}</span>
          <span v-if="data.personal.linkedin || data.personal.website" class="separator">·</span>
        </template>
        <template v-if="data.personal.linkedin">
          <span>{{ data.personal.linkedin }}</span>
          <span v-if="data.personal.website" class="separator">·</span>
        </template>
        <template v-if="data.personal.website">
          <span>{{ data.personal.website }}</span>
        </template>
        </div>
      </div>
    </header>

    <section v-if="data.personal.summary" class="cv-section">
      <p class="summary">{{ data.personal.summary }}</p>
    </section>

    <section v-if="data.experience.length" class="cv-section">
      <h2>Experience</h2>
      <div v-for="exp in data.experience" :key="exp.id" class="item">
        <div class="item-top">
          <span class="title">{{ exp.position }}</span>
          <span class="company">{{ exp.company }}</span>
        </div>
        <span class="date">{{ exp.startDate }} — {{ exp.endDate }}</span>
        <p>{{ exp.description }}</p>
      </div>
    </section>

    <section v-if="data.education.length" class="cv-section">
      <h2>Education</h2>
      <div v-for="edu in data.education" :key="edu.id" class="item">
        <div class="item-top">
          <span class="title">{{ edu.degree }} {{ edu.field ? 'in ' + edu.field : '' }}</span>
          <span class="company">{{ edu.institution }}</span>
        </div>
        <span class="date">{{ edu.startDate }} — {{ edu.endDate }}</span>
      </div>
    </section>

    <section v-if="data.skills.length" class="cv-section">
      <h2>Skills</h2>
      <p class="skills">
        <span v-for="(skill, index) in data.skills" :key="skill.id">
          {{ skill.name }}<span v-if="skill.level">({{ skill.level }})</span><span v-if="index < data.skills.length - 1">, </span>
        </span>
      </p>
    </section>

    <section v-if="data.projects.length" class="cv-section">
      <h2>Projects</h2>
      <div v-for="project in data.projects" :key="project.id" class="item">
        <div class="item-top">
          <span class="title">{{ project.name }}</span>
          <span v-if="project.link" class="link">{{ project.link }}</span>
        </div>
        <p>{{ project.description }}</p>
        <p v-if="project.technologies" class="technologies">{{ project.technologies }}</p>
      </div>
    </section>

    <section v-if="data.certifications.length" class="cv-section">
      <h2>Certifications</h2>
      <div v-for="cert in data.certifications" :key="cert.id" class="item">
        <div class="item-top">
          <span class="title">{{ cert.name }}</span>
          <span class="company">{{ cert.issuer }}</span>
        </div>
        <span class="date">{{ cert.date }}</span>
      </div>
    </section>

    <section v-if="data.languages.length" class="cv-section">
      <h2>Languages</h2>
      <p class="skills">
        <span v-for="(lang, index) in data.languages" :key="lang.id">
          {{ lang.name }} ({{ lang.level }})<span v-if="index < data.languages.length - 1">, </span>
        </span>
      </p>
    </section>

    <section v-if="data.exams && data.exams.length" class="cv-section">
      <h2>Examinations</h2>
      <div v-for="exam in data.exams" :key="exam.id" class="exam-block">
        <div class="exam-header">
          <span class="exam-title">{{ exam.name }}</span>
          <span class="exam-meta">{{ exam.year }} {{ exam.place ? '• ' + exam.place : '' }}</span>
        </div>
        <div class="exam-subjects">
          <span v-for="(subject, index) in exam.subjects" :key="index" class="subject-tag">
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
</template>

<script>
export default {
  name: 'MinimalTemplate',
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
  padding: 50px;
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  font-size: 10pt;
  line-height: 1.6;
  color: #222;
  width: 210mm;
  min-height: 297mm;
  background: #fff;
  box-sizing: border-box;
}

.cv-header {
  text-align: center;
  margin-bottom: 30px;
}

.cv-header {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.profile-image {
  width: 100px;
  height: 100px;
  margin-bottom: 16px;
}

.profile-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
}

.header-text {
  text-align: center;
}

.cv-header h1 {
  font-size: 24pt;
  font-weight: 300;
  margin: 0 0 10px;
  letter-spacing: 2px;
}

.contact-info {
  font-size: 9pt;
  color: #666;
}

.separator {
  margin: 0 6px;
}

.cv-section {
  margin-bottom: 24px;
  page-break-inside: avoid;
}

.cv-section h2 {
  font-size: 10pt;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  margin: 0 0 16px;
  color: #999;
}

.summary {
  font-size: 10pt;
  line-height: 1.7;
  color: #444;
}

.item {
  margin-bottom: 16px;
}

.item-top {
  margin-bottom: 2px;
}

.title {
  font-weight: 600;
  margin-right: 8px;
}

.company {
  color: #666;
}

.date {
  font-size: 9pt;
  color: #888;
}

.item p {
  margin: 6px 0 0;
  color: #444;
}

.skills {
  color: #444;
}

.technologies {
  font-size: 9pt;
  color: #888;
  margin-top: 4px;
}

.link {
  font-size: 9pt;
  color: #666;
}

.exam-block {
  margin-bottom: 16px;
}

.exam-header {
  margin-bottom: 4px;
}

.exam-title {
  font-weight: 600;
  margin-right: 8px;
}

.exam-meta {
  font-size: 9pt;
  color: #888;
}

.exam-subjects {
  font-size: 9pt;
  color: #555;
}

.subject-tag {
  white-space: nowrap;
}
</style>
