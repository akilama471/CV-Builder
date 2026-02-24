<template>
  <div class="cv-template classic">
    <header class="cv-header">
      <div v-if="data.personal.image" class="profile-image">
        <img :src="data.personal.image" alt="Profile" />
      </div>
      <h1>{{ data.personal.fullName }}</h1>
      <div class="contact-info">
        <span v-if="data.personal.email">{{ data.personal.email }}</span>
        <span v-if="data.personal.phone">{{ data.personal.phone }}</span>
        <span v-if="data.personal.address">{{ data.personal.address }}</span>
        <span v-if="data.personal.linkedin">{{ data.personal.linkedin }}</span>
        <span v-if="data.personal.website">{{ data.personal.website }}</span>
      </div>
    </header>

    <section v-if="data.personal.summary" class="cv-section">
      <h2>Summary</h2>
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
        <div>{{ edu.degree }} in {{ edu.field }}</div>
      </div>
    </section>

    <section v-if="data.skills.length" class="cv-section">
      <h2>Skills</h2>
      <div class="skills-list">
        <span v-for="skill in data.skills" :key="skill.id" class="skill-tag">
          {{ skill.name }}<span v-if="skill.level"> - {{ skill.level }}</span>
        </span>
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
        <div v-if="project.technologies" class="technologies">Technologies: {{ project.technologies }}</div>
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
        <div class="subjects-grid">
          <div v-for="(subject, index) in exam.subjects" :key="index" class="subject-entry">
            <span class="subject-name">{{ subject.name }}</span>
            <span class="subject-marks">{{ subject.marks }}</span>
          </div>
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
  name: 'ClassicTemplate',
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
  padding: 40px;
  font-family: 'Georgia', serif;
  font-size: 11pt;
  line-height: 1.5;
  color: #333;
  width: 210mm;
  min-height: 297mm;
  background: #fff;
  box-sizing: border-box;
}

.cv-header {
  display: flex;
  align-items: center;
  gap: 20px;
  border-bottom: 2px solid #333;
  padding-bottom: 20px;
  margin-bottom: 24px;
}

.profile-image {
  width: 100px;
  height: 100px;
  flex-shrink: 0;
}

.profile-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 4px;
}

.cv-header h1 {
  margin: 0 0 10px;
  font-size: 28pt;
  color: #1a1a1a;
}

.contact-info {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  font-size: 10pt;
}

.contact-info span {
  color: #555;
}

.cv-section {
  margin-bottom: 24px;
  page-break-inside: avoid;
}

.cv-section h2 {
  font-size: 14pt;
  text-transform: uppercase;
  letter-spacing: 1px;
  border-bottom: 1px solid #ccc;
  padding-bottom: 6px;
  margin: 0 0 16px;
  color: #1a1a1a;
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
}

.date {
  font-size: 10pt;
  color: #666;
}

.company {
  font-style: italic;
  color: #555;
  margin-bottom: 8px;
}

.experience-item,
.education-item,
.project-item,
.cert-item {
  margin-bottom: 16px;
}

.skills-list,
.languages-list,
.exam-scores-list {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.skill-tag,
.language-tag {
  background: #f0f0f0;
  padding: 4px 12px;
  border-radius: 4px;
  font-size: 10pt;
}

.exam-item {
  margin-bottom: 18px;
}

.subjects-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 8px;
  margin-top: 8px;
}

.subject-entry {
  display: flex;
  justify-content: space-between;
  background: #f8f8f8;
  padding: 4px 10px;
  border-radius: 4px;
  font-size: 10pt;
}

.subject-name {
  color: #555;
}

.subject-marks {
  font-weight: 500;
}

.exam-score {
  font-size: 10pt;
  color: #666;
  margin-top: 4px;
}

.link {
  font-size: 10pt;
  color: #0066cc;
}
</style>
