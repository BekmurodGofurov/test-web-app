<template>
    <div>
      <h1 class="text-center mb-4">Dasturlash Tillari</h1>
  
      <!-- Dasturlash tillari ro'yxatini chiqaramiz -->
      <div class="row">
        <div v-for="course in courses" :key="course.name" class="col-md-4 mb-3 ">
          <div class="card h-100 background-card " @click="selectCourse(course)">
            <div class="card-body">
              <h5 class="card-title ">{{ course.name }}</h5>
              <p class="card-text">{{ course.description }}</p>
              <a href="#lessons" class="btn btn-primary" @click="selectCourse(course)">Darslarni ko'rish</a>
            </div>
          </div>
        </div>
      </div>
  
      <!-- Darslar qismi (foydalanuvchi dasturlash tilini tanlaganida ko'rsatiladi) -->
      <div v-if="selectedCourse" class="mb-3" id="lessons">
        <h1 class="text-center mt-4">{{ selectedCourse.name }} Darslari</h1>
        <ul class="list-group">
          <li v-for="lesson in selectedCourse.lessons" :key="lesson" class="background-card list-group-item d-flex justify-content-between align-items-center ">
            {{ lesson }}
            <button class="btn btn-primary" @click="$emit('start-learning', lesson)">Boshlash</button>
          </li>
        </ul>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        courses: [
          {
            name: "Python",
            description: "Python - Kuchli va mashhur dasturlash tili",
            lessons: ["Python Kirish", "Python Sintaksisi", "O'zgaruvchilar"]
          },
          {
            name: "JavaScript",
            description: "JavaScript - Web dasturlash tili",
            lessons: ["JS Kirish", "JS Funktsiyalar", "DOM Manipulyatsiya"]
          },
          {
            name: "Java",
            description: "Java - OOP ning asosiy tillaridan biri",
            lessons: ["Java Kirish", "Java Sintaksisi", "Java Klasslar"]
          },
        ],
        selectedCourse: null
      };
    },
    methods: {
      selectCourse(course) {
        this.selectedCourse = course;
      }
    }
  };
  </script>
  
  <style>

  .background-card{
    background-color: transparent !important;
    border: 2px solid #42089e;
  }

  .card-text {
    color: #bab7bd;
  }

  .card {
    cursor: pointer;
    transition: transform 0.2s ease-in-out;
  }
  
  .card:hover {
    transform: scale(1.05);
  }
  </style>
  