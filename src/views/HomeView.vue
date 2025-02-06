<template>
  <div class="min-vh-100 bg-light">
    <!-- Enhanced Navigation -->
    <nav class="navbar navbar-expand-lg bg-white shadow-sm fixed-top">
      <div class="container">
        <a class="navbar-brand fs-3 fw-bold text-dark" href="#">
          <span class="gradient-text">Vasvári</span>App
        </a>
        <div class="d-flex align-items-center gap-3">
          <!-- Show login button on smaller screens -->
          <button class="btn btn-gradient-primary rounded-pill px-4 fw-semibold hover-lift d-lg-none">
            Bejelentkezés <i class="bi bi-arrow-right ms-2"></i>
          </button>
          <a href="https://vasvari.hu" target="_blank" class="nav-link text-secondary hover-gradient d-none d-lg-block">
            Vasvári Weblap <i class="bi bi-box-arrow-up-right ms-1"></i>
          </a>
          <!-- Hide login button on smaller screens -->
          <button class="btn btn-gradient-primary rounded-pill px-4 fw-semibold hover-lift d-none d-lg-block">
            Bejelentkezés <i class="bi bi-arrow-right ms-2"></i>
          </button>
        </div>
      </div>
    </nav>

    <!-- Enhanced Hero Section -->
    <header class="gradient-section vh-md-auto">
      <div class="container">
        <div class="row align-items-center py-5 vh-100 ">
          <div class="col-lg-6 text-center text-lg-start mb-5 mb-lg-0">
            <h1 class="display-3 fw-bold mb-4 animate-slide-up">
              Üdvözöllek a<br><span class="gradient-text">VasváriApp</span>-nál
            </h1>
            <p class="lead mb-5 fs-5 text-light">Egyszerű módja az órarend kezelésére</p>
            <div class="d-flex flex-column flex-sm-row gap-3 justify-content-center justify-content-lg-start">
              <button class="btn btn-light btn-hover-grow rounded-pill px-5 py-3 fw-bold shadow-sm">
                <i class="bi bi-box-arrow-in-right me-2"></i>Bejelentkezés
              </button>
              <button class="btn btn-outline-light btn-hover-grow rounded-pill px-5 py-3 fw-bold">
                
                <i class="bi bi-download me-2"></i>Mobil App
              </button>
            </div>
          </div>
          <div class="col-lg-6">
            <!-- Original Phone Container -->
            <div class="phone-container d-none d-md-block">
              <div class="phone">
                <div class="phone-screen">
                  <img src="../assets/phone_screen_img.png" alt="App screenshot" class="phone-screenshot w-100 h-100 rounded">
                </div>
              </div>
            </div>
            <!-- Show image only on mobile view with phone-like border -->
            <div class="mobile-phone-border d-block d-md-none">
              <img src="../assets/phone_screen_img.png" alt="App screenshot" class="w-100 h-100 rounded">
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Enhanced Features Section -->
    <section class="py-6 bg-white">
      <div class="container">
        <h2 class="text-center display-4 fw-bold mb-6 animate-slide-up">
          <span class="gradient-text">Funkciók</span>
        </h2>
        <div class="row g-4">
          <div v-for="(feature, index) in features" :key="feature.title" 
               class="col-md-4" :style="`transition-delay: ${index * 50}ms`">
            <div class="card h-100 p-4 border-0 shadow-sm hover-lift bg-soft-primary">
              <div class="icon-wrapper bg-gradient-primary shadow">
                <component :is="feature.icon" style="width: 32px; height: 32px" />
              </div>
              <h3 class="h4 fw-semibold mt-4 mb-3">{{ feature.title }}</h3>
              <p class="text-body-secondary">{{ feature.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
<script setup>
import { ref } from 'vue';
import { CalendarSync, Newspaper, Info } from 'lucide-vue-next';

const features = [
  {
    icon: CalendarSync,
    title: 'Dinamikus Órarend',
    description: 'Egy folyamatosan frissülő órarend, amely egyszerűen kezelhető és mindig naprakész.'
  },
  {
    icon: Newspaper,
    title: 'Hírfal',
    description: 'Tudd meg elsőként az iskolai eseményeket és legfrissebb híreket!'
  },
  {
    icon: Info,
    title: 'Hasznos infók',
    description: 'Minden fontos információ egy helyen: iskolai tudnivalók, dokumentumok és szünetek.'
  }
];
</script>
<style>
/* Keep original phone styles */
.phone-container {
  perspective: 1000px;
  transform-style: preserve-3d;
  width: 100%;
  max-width: 330px;
  margin: 0 auto;
  position: relative;
  filter: drop-shadow(15px 20px 40px rgba(0, 0, 0, 0.6));
}

.phone {
  width: 100%;
  padding-bottom: 215%;
  position: relative;
  transform: rotateY(-20deg) rotateX(10deg) rotateZ(-2deg);
  transition: transform 0.3s ease;
}

.phone:hover {
  transform: rotateY(-15deg) rotateX(5deg) rotateZ(-1deg) scale(1.02);
}

.phone-screen {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: #000;
  border-radius: 40px;
  border: 8px solid #333;
  overflow: hidden;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
}

/* Further adjust phone size for mobile view */
@media (max-width: 768px) {
  .phone-container {
    max-width: 150px;
      box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);

  }
}

/* Mobile phone-like border */
.mobile-phone-border {
  position: relative;
  width: 100%;
  max-width: 250px;
  margin: 0 auto;
  border-radius: 15px;
  border: 4px solid #333;
  overflow: hidden;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
}

/* Adjust hero section height for mobile view */
@media (max-width: 768px) {
  .vh-md-auto {
    margin-top: 60px;
    height: 130vh;
  }
}

/* Enhanced other elements */
.gradient-text {
  background: linear-gradient(45deg, #6B46E1, #8A4BFF);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.gradient-section {
  background: linear-gradient(135deg, #4a1d6b, #8a4baf);
}

.btn-gradient-primary {
  background: linear-gradient(45deg, #8746ef, #6b2ee3);
  border: none;
  color: white !important;
  transition: all 0.3s ease;
}

.hover-lift {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.hover-lift:hover {
  transform: translateY(-5px);
  box-shadow: 0 12px 24px rgba(107, 70, 225, 0.25);
}

.bg-soft-primary {
  background: rgba(107, 70, 225, 0.05);
}

.icon-wrapper {
  width: 64px;
  height: 64px;
  border-radius: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.animate-slide-up {
  opacity: 0;
  transform: translateY(20px);
  animation: slideUp 0.6s cubic-bezier(0.22, 0.61, 0.36, 1) forwards;
}

@keyframes slideUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.btn-hover-grow {
  transition: transform 0.2s ease;
}

.btn-hover-grow:hover {
  transform: scale(1.05);
}

.hover-gradient {
  position: relative;
  transition: color 0.3s ease;
}

.hover-gradient::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(45deg, #6B46E1, #8A4BFF);
  transition: width 0.3s ease;
}

.hover-gradient:hover::after {
  width: 100%;
}
</style>