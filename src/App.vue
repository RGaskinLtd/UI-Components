<template>
  <div id="app">
    <HeroSlider
      :slides="heroSlides"
      :autoplay="true"
      :interval="5000"
      @button-click="handleSlideButtonClick"
    />
  </div>
</template>

<script>
import HeroSlider from './components/HeroSlider.vue';

export default {
  name: 'App',
  components: {
    HeroSlider
  },
  data() {
    return {
      heroSlides: [
        {
          title: 'Welcome to Our Platform',
          description: 'Discover amazing features and endless possibilities',
          image: 'https://images.unsplash.com/photo-1557683316-973673baf926?w=1920&q=80',
          buttonText: 'Get Started'
        },
        {
          title: 'Build Something Amazing',
          description: 'Create beautiful experiences with our tools',
          image: 'https://images.unsplash.com/photo-1451187580459-43490279c0fa?w=1920&q=80',
          buttonText: 'Learn More'
        },
        {
          title: 'Join Our Community',
          description: 'Connect with thousands of developers worldwide',
          image: 'https://images.unsplash.com/photo-1522071820081-009f0129c71c?w=1920&q=80',
          buttonText: 'Join Now'
        }
      ]
    };
  },
  methods: {
    handleSlideButtonClick(event) {
      console.log('Button clicked on slide:', event.slideIndex);
      console.log('Slide data:', event.slide);
      // Handle button click logic here
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

#app {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  width: 100vw;
  height: 100vh;
}
</style>
