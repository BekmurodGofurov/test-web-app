<template>
  <div id="app" class="container mt-5">
    <!-- Tugmalarni o'rtaga joylashtirish uchun "text-center" sinfidan foydalanamiz -->
    <div class="text-center mb-4">
      <button class="btn btn-outline-primary mr-4 but" @click="currentSection = 'all'">Home</button>
      <button class="btn btn-outline-primary mr-4 but" @click="currentSection = 'learning'">Learning</button>
      <button class="btn btn-outline-primary but" @click="currentSection = 'completed'">Done</button>
    </div>

    <!-- Komponentlar uchun qo'ng'iroqlar -->
    <AllCourses v-if="currentSection === 'all'" @start-learning="startLearning" />
    <LearningCourses v-if="currentSection === 'learning'" :lessons="learningLessons" @complete="completeLesson" />
    <CompletedCourses v-if="currentSection === 'completed'" :lessons="completedLessons" />
  </div>
</template>

<script>
import AllCourses from './components/AllCourses.vue';
import LearningCourses from './components/LearningCourses.vue';
import CompletedCourses from './components/CompletedCourses.vue';

export default {
  components: {
    AllCourses,
    LearningCourses,
    CompletedCourses
  },
  data() {
    return {
      currentSection: 'all',
      learningLessons: [],
      completedLessons: []
    };
  },
  methods: {
    startLearning(lesson) {
      this.learningLessons.push(lesson);
      this.currentSection = 'learning';
      const data = { lesson: lesson, status: 'learning' };
      window.Telegram.WebApp.sendData(JSON.stringify(data));
    },
    completeLesson(lesson) {
      this.completedLessons.push(lesson);
      this.learningLessons = this.learningLessons.filter(l => l !== lesson);
      const data = { lesson: lesson, status: 'completed' };
      window.Telegram.WebApp.sendData(JSON.stringify(data));
    }
  },
  mounted() {
    window.Telegram.WebApp.ready();
  }
};
</script>


<style>
.but{
  font-size: 24px;
}

#app {
  font-family: Arial, sans-serif;
}
</style>
