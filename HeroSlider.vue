<template>
  <div class="hero-slider">
    <div class="slider-container">
      <!-- Slides -->
      <transition-group name="slide" tag="div" class="slides">
        <div
          v-for="(slide, index) in slides"
          v-show="index === currentSlide"
          :key="slide.id"
          class="slide"
          :style="{ backgroundImage: `url(${slide.image})` }"
        >
          <div class="slide-content">
            <h1 v-if="slide.title" class="slide-title">{{ slide.title }}</h1>
            <p v-if="slide.description" class="slide-description">{{ slide.description }}</p>
            <button
              v-if="slide.buttonText"
              class="slide-button"
              @click="handleButtonClick(slide)"
            >
              {{ slide.buttonText }}
            </button>
          </div>
        </div>
      </transition-group>

      <!-- Navigation Arrows -->
      <button
        v-if="showArrows"
        class="arrow arrow-left"
        @click="previousSlide"
        aria-label="Previous slide"
      >
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <polyline points="15 18 9 12 15 6"></polyline>
        </svg>
      </button>
      <button
        v-if="showArrows"
        class="arrow arrow-right"
        @click="nextSlide"
        aria-label="Next slide"
      >
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <polyline points="9 18 15 12 9 6"></polyline>
        </svg>
      </button>

      <!-- Dots Indicator -->
      <div v-if="showDots" class="dots">
        <button
          v-for="(slide, index) in slides"
          :key="'dot-' + slide.id"
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
        return slides.every(slide => slide.id && slide.image);
      }
    },
    autoplay: {
      type: Boolean,
      default: true
    },
    autoplaySpeed: {
      type: Number,
      default: 5000
    },
    showArrows: {
      type: Boolean,
      default: true
    },
    showDots: {
      type: Boolean,
      default: true
    }
  },
  data() {
    return {
      currentSlide: 0,
      autoplayInterval: null
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
    previousSlide() {
      this.currentSlide = (this.currentSlide - 1 + this.slides.length) % this.slides.length;
      this.resetAutoplay();
    },
    goToSlide(index) {
      this.currentSlide = index;
      this.resetAutoplay();
    },
    startAutoplay() {
      if (this.autoplay) {
        this.autoplayInterval = setInterval(() => {
          this.nextSlide();
        }, this.autoplaySpeed);
      }
    },
    stopAutoplay() {
      if (this.autoplayInterval) {
        clearInterval(this.autoplayInterval);
        this.autoplayInterval = null;
      }
    },
    resetAutoplay() {
      this.stopAutoplay();
      this.startAutoplay();
    },
    handleButtonClick(slide) {
      this.$emit('button-click', slide);
    }
  }
};
</script>

<style scoped>
.hero-slider {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
}

.slider-container {
  width: 100%;
  height: 100%;
  position: relative;
}

.slides {
  width: 100%;
  height: 100%;
  position: relative;
}

.slide {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background-size: cover;
  background-position: center;
  display: flex;
  align-items: center;
  justify-content: center;
}

.slide-content {
  text-align: center;
  color: white;
  padding: 2rem;
  max-width: 800px;
  z-index: 1;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.slide-title {
  font-size: 3rem;
  font-weight: bold;
  margin-bottom: 1rem;
  animation: fadeInUp 0.8s ease-out;
}

.slide-description {
  font-size: 1.5rem;
  margin-bottom: 2rem;
  animation: fadeInUp 0.8s ease-out 0.2s backwards;
}

.slide-button {
  padding: 1rem 2rem;
  font-size: 1.1rem;
  background-color: rgba(255, 255, 255, 0.2);
  color: white;
  border: 2px solid white;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
  animation: fadeInUp 0.8s ease-out 0.4s backwards;
}

.slide-button:hover {
  background-color: white;
  color: #333;
  transform: translateY(-2px);
}

/* Arrows */
.arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(255, 255, 255, 0.3);
  border: none;
  color: white;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.arrow:hover {
  background-color: rgba(255, 255, 255, 0.5);
  transform: translateY(-50%) scale(1.1);
}

.arrow-left {
  left: 2rem;
}

.arrow-right {
  right: 2rem;
}

.arrow svg {
  width: 24px;
  height: 24px;
}

/* Dots */
.dots {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 0.75rem;
  z-index: 10;
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.5);
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
}

.dot:hover {
  background-color: rgba(255, 255, 255, 0.8);
  transform: scale(1.2);
}

.dot.active {
  background-color: white;
  width: 32px;
  border-radius: 6px;
}

/* Transitions */
.slide-enter-active,
.slide-leave-active {
  transition: opacity 0.5s ease;
}

.slide-enter-from {
  opacity: 0;
}

.slide-leave-to {
  opacity: 0;
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
    font-size: 1.1rem;
  }

  .arrow {
    width: 40px;
    height: 40px;
  }

  .arrow-left {
    left: 1rem;
  }

  .arrow-right {
    right: 1rem;
  }

  .dots {
    bottom: 1rem;
  }
}

@media (max-width: 480px) {
  .slide-title {
    font-size: 1.5rem;
  }

  .slide-description {
    font-size: 1rem;
  }

  .slide-content {
    padding: 1rem;
  }
}
</style>
