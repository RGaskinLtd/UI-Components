<template>
  <div class="hero-slider">
    <div class="slider-container">
      <transition :name="transitionName" mode="out-in">
        <div
          :key="currentSlide"
          class="slide"
          :style="{ backgroundImage: `url(${slides[currentSlide].image})` }"
        >
          <div class="slide-content">
            <h1 class="slide-title">{{ slides[currentSlide].title }}</h1>
            <p class="slide-description">{{ slides[currentSlide].description }}</p>
            <button
              v-if="slides[currentSlide].buttonText"
              class="slide-button"
              @click="handleButtonClick(currentSlide)"
            >
              {{ slides[currentSlide].buttonText }}
            </button>
          </div>
        </div>
      </transition>

      <!-- Navigation Arrows -->
      <button class="nav-arrow prev" @click="prevSlide" aria-label="Previous slide">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <polyline points="15 18 9 12 15 6"></polyline>
        </svg>
      </button>
      <button class="nav-arrow next" @click="nextSlide" aria-label="Next slide">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <polyline points="9 18 15 12 9 6"></polyline>
        </svg>
      </button>

      <!-- Dots Navigation -->
      <div class="dots-container">
        <button
          v-for="(slide, index) in slides"
          :key="index"
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
          slide.hasOwnProperty('title') &&
          slide.hasOwnProperty('image')
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
      transitionName: 'slide-fade',
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
      this.transitionName = 'slide-fade';
      this.currentSlide = (this.currentSlide + 1) % this.slides.length;
      this.resetAutoplay();
    },
    prevSlide() {
      this.transitionName = 'slide-fade-reverse';
      this.currentSlide = this.currentSlide === 0
        ? this.slides.length - 1
        : this.currentSlide - 1;
      this.resetAutoplay();
    },
    goToSlide(index) {
      if (index !== this.currentSlide) {
        this.transitionName = index > this.currentSlide
          ? 'slide-fade'
          : 'slide-fade-reverse';
        this.currentSlide = index;
        this.resetAutoplay();
      }
    },
    handleButtonClick(index) {
      this.$emit('button-click', {
        slideIndex: index,
        slide: this.slides[index]
      });
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
  height: 100%;
  position: relative;
  overflow: hidden;
}

.slider-container {
  width: 100%;
  height: 100%;
  position: relative;
}

.slide {
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.slide::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.4);
  z-index: 1;
}

.slide-content {
  position: relative;
  z-index: 2;
  text-align: center;
  color: white;
  max-width: 800px;
  padding: 2rem;
}

.slide-title {
  font-size: 3.5rem;
  font-weight: bold;
  margin-bottom: 1rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.slide-description {
  font-size: 1.5rem;
  margin-bottom: 2rem;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
}

.slide-button {
  padding: 1rem 2.5rem;
  font-size: 1.1rem;
  font-weight: 600;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
}

.slide-button:hover {
  background-color: #2980b9;
  transform: translateY(-2px);
  box-shadow: 0 6px 8px rgba(0, 0, 0, 0.4);
}

.nav-arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(255, 255, 255, 0.3);
  color: white;
  border: none;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
  z-index: 10;
}

.nav-arrow:hover {
  background-color: rgba(255, 255, 255, 0.5);
}

.nav-arrow.prev {
  left: 2rem;
}

.nav-arrow.next {
  right: 2rem;
}

.dots-container {
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

.dot.active {
  background-color: white;
  width: 40px;
  border-radius: 6px;
}

.dot:hover {
  background-color: rgba(255, 255, 255, 0.8);
}

/* Transitions */
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.6s ease;
}

.slide-fade-enter-from {
  opacity: 0;
  transform: translateX(100px);
}

.slide-fade-leave-to {
  opacity: 0;
  transform: translateX(-100px);
}

.slide-fade-reverse-enter-active,
.slide-fade-reverse-leave-active {
  transition: all 0.6s ease;
}

.slide-fade-reverse-enter-from {
  opacity: 0;
  transform: translateX(-100px);
}

.slide-fade-reverse-leave-to {
  opacity: 0;
  transform: translateX(100px);
}

/* Responsive Design */
@media (max-width: 768px) {
  .slide-title {
    font-size: 2rem;
  }

  .slide-description {
    font-size: 1rem;
  }

  .nav-arrow {
    width: 40px;
    height: 40px;
  }

  .nav-arrow.prev {
    left: 1rem;
  }

  .nav-arrow.next {
    right: 1rem;
  }

  .slide-button {
    padding: 0.75rem 1.5rem;
    font-size: 1rem;
  }
}
</style>
