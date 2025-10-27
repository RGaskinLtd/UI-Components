<template>
  <div id="app">
    <HeroSlider
      :slides="heroSlides"
      :autoplay="true"
      :interval="5000"
      @button-click="handleButtonClick"
    />
  </div>
</template>

<script>
import HeroSlider from './HeroSlider.vue';

export default {
  name: 'App',
  components: {
    HeroSlider
  },
  data() {
    return {
      heroSlides: [
        {
          id: 1,
          title: 'Welcome to Our Amazing Product',
          description: 'Discover the future of innovation with our cutting-edge solutions',
          image: 'https://images.unsplash.com/photo-1497436072909-60f360e1d4b1?w=1920&h=1080&fit=crop',
          buttonText: 'Get Started',
          link: '/get-started'
        },
        {
          id: 2,
          title: 'Build Something Great',
          description: 'Transform your ideas into reality with powerful tools',
          image: 'https://images.unsplash.com/photo-1519681393784-d120267933ba?w=1920&h=1080&fit=crop',
          buttonText: 'Learn More',
          link: '/learn-more'
        },
        {
          id: 3,
          title: 'Join Our Community',
          description: 'Connect with thousands of developers worldwide',
          image: 'https://images.unsplash.com/photo-1504384308090-c894fdcc538d?w=1920&h=1080&fit=crop',
          buttonText: 'Sign Up',
          link: '/signup'
        }
      ]
    };
  },
  methods: {
    handleButtonClick(slide) {
      console.log('Button clicked for slide:', slide);
      // Handle navigation or other actions
      // this.$router.push(slide.link);
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
}

#app {
  width: 100%;
  height: 100vh;
}
</style>
