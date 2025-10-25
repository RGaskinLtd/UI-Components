<template>
  <section class="hero-banner" :style="bannerStyle">
    <div class="hero-content">
      <h1 v-if="title" class="hero-title">{{ title }}</h1>
      <p v-if="subtitle" class="hero-subtitle">{{ subtitle }}</p>
      <div v-if="$slots.default" class="hero-actions">
        <slot></slot>
      </div>
    </div>
    <div v-if="overlay" class="hero-overlay"></div>
  </section>
</template>

<script>
export default {
  name: 'HeroBanner',
  props: {
    title: {
      type: String,
      default: 'Welcome to Our Site'
    },
    subtitle: {
      type: String,
      default: 'Discover amazing content and experiences'
    },
    backgroundImage: {
      type: String,
      default: ''
    },
    backgroundColor: {
      type: String,
      default: '#667eea'
    },
    height: {
      type: String,
      default: '500px'
    },
    overlay: {
      type: Boolean,
      default: true
    }
  },
  computed: {
    bannerStyle() {
      const styles = {
        height: this.height
      };

      if (this.backgroundImage) {
        styles.backgroundImage = `url(${this.backgroundImage})`;
      } else {
        styles.backgroundColor = this.backgroundColor;
      }

      return styles;
    }
  }
}
</script>

<style scoped>
.hero-banner {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  overflow: hidden;
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.4);
  z-index: 1;
}

.hero-content {
  position: relative;
  z-index: 2;
  text-align: center;
  color: white;
  padding: 2rem;
  max-width: 800px;
}

.hero-title {
  font-size: 3rem;
  font-weight: bold;
  margin: 0 0 1rem 0;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.hero-subtitle {
  font-size: 1.5rem;
  margin: 0 0 2rem 0;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3);
}

.hero-actions {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

@media (max-width: 768px) {
  .hero-title {
    font-size: 2rem;
  }

  .hero-subtitle {
    font-size: 1.2rem;
  }

  .hero-content {
    padding: 1rem;
  }
}
</style>
