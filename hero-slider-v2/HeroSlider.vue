<template>
  <div class="hero-slider">
    <div class="slider-container">
      <transition-group name="slide" tag="div" class="slides-wrapper">
        <div
          v-for="(slide, index) in slides"
          :key="slide.id"
          v-show="index === currentSlide"
          class="slide"
          :style="{ backgroundImage: `url(${slide.image})` }"
        >
          <div class="slide-content">
            <h1 class="slide-title">{{ slide.title }}</h1>
            <p class="slide-description">{{ slide.description }}</p>
            <button v-if="slide.buttonText" class="slide-button" @click="handleButtonClick(slide)">
              {{ slide.buttonText }}
            </button>
          </div>
        </div>
      </transition-group>

      <!-- Navigation Arrows -->
      <button class="nav-button prev" @click="prevSlide" aria-label="Previous slide">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M15 18L9 12L15 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </button>
      <button class="nav-button next" @click="nextSlide" aria-label="Next slide">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M9 18L15 12L9 6" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </button>

      <!-- Dots Navigation -->
      <div class="dots-container">
        <button
          v-for="(slide, index) in slides"
          :key="`dot-${slide.id}`"
          class="dot"
          :class="{ active: index === currentSlide }"
          @click="goToSlide(index)"
          :aria-label="`Go to slide ${index + 1}`"
        ></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HeroSlider',
  props: {
    slides: {
      type: Array,
      required: true,
      validator: (slides) => {
        return slides.every(slide =>
          slide.id && slide.title && slide.image
        );
      }
    },
    autoplay: {
      type: Boolean,
      default: true
    },
    interval: {
      type: Number,
      default: 5000
    }
  },
  data() {
    return {
      currentSlide: 0,
      autoplayTimer: null
    };
  },
  mounted() {
    if (this.autoplay) {
      this.startAutoplay();
    }
  },
  beforeUnmount() {
    this.stopAutoplay();
  },
  methods: {
    nextSlide() {
      this.currentSlide = (this.currentSlide + 1) % this.slides.length;
      this.resetAutoplay();
    },
    prevSlide() {
      this.currentSlide = this.currentSlide === 0
        ? this.slides.length - 1
        : this.currentSlide - 1;
      this.resetAutoplay();
    },
    goToSlide(index) {
      this.currentSlide = index;
      this.resetAutoplay();
    },
    handleButtonClick(slide) {
      this.$emit('button-click', slide);
    },
    startAutoplay() {
      this.autoplayTimer = setInterval(() => {
        this.nextSlide();
      }, this.interval);
    },
    stopAutoplay() {
      if (this.autoplayTimer) {
        clearInterval(this.autoplayTimer);
        this.autoplayTimer = null;
      }
    },
    resetAutoplay() {
      if (this.autoplay) {
        this.stopAutoplay();
        this.startAutoplay();
      }
    }
  }
};
</script>

<style scoped>
.hero-slider {
  width: 100%;
  height: 100vh;
  overflow: hidden;
  position: relative;
}

.slider-container {
  width: 100%;
  height: 100%;
  position: relative;
}

.slides-wrapper {
  width: 100%;
  height: 100%;
  position: relative;
}

.slide {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  display: flex;
  align-items: center;
  justify-content: center;
}

.slide::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.4);
  z-index: 1;
}

.slide-content {
  position: relative;
  z-index: 2;
  text-align: center;
  color: white;
  max-width: 800px;
  padding: 20px;
}

.slide-title {
  font-size: 3.5rem;
  font-weight: bold;
  margin-bottom: 1rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
  animation: fadeInUp 0.8s ease-out;
}

.slide-description {
  font-size: 1.5rem;
  margin-bottom: 2rem;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
  animation: fadeInUp 0.8s ease-out 0.2s both;
}

.slide-button {
  padding: 15px 40px;
  font-size: 1.1rem;
  font-weight: 600;
  color: white;
  background-color: #007bff;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  animation: fadeInUp 0.8s ease-out 0.4s both;
}

.slide-button:hover {
  background-color: #0056b3;
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(0, 123, 255, 0.4);
}

/* Navigation Buttons */
.nav-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(255, 255, 255, 0.2);
  border: none;
  color: white;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  z-index: 10;
  backdrop-filter: blur(10px);
}

.nav-button:hover {
  background: rgba(255, 255, 255, 0.4);
  transform: translateY(-50%) scale(1.1);
}

.nav-button.prev {
  left: 30px;
}

.nav-button.next {
  right: 30px;
}

/* Dots Navigation */
.dots-container {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 12px;
  z-index: 10;
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.5);
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
}

.dot:hover {
  background: rgba(255, 255, 255, 0.8);
  transform: scale(1.2);
}

.dot.active {
  background: white;
  width: 30px;
  border-radius: 6px;
}

/* Slide Transitions */
.slide-enter-active,
.slide-leave-active {
  transition: all 0.8s ease;
}

.slide-enter-from {
  opacity: 0;
  transform: translateX(100%);
}

.slide-leave-to {
  opacity: 0;
  transform: translateX(-100%);
}

/* Animations */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Responsive Design */
@media (max-width: 768px) {
  .slide-title {
    font-size: 2rem;
  }

  .slide-description {
    font-size: 1rem;
  }

  .slide-button {
    padding: 12px 30px;
    font-size: 1rem;
  }

  .nav-button {
    width: 40px;
    height: 40px;
  }

  .nav-button.prev {
    left: 15px;
  }

  .nav-button.next {
    right: 15px;
  }
}
</style>
