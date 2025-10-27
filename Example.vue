<template>
  <div id="app">
    <HeroSlider
      :slides="heroSlides"
      :autoplay="true"
      :autoplay-speed="5000"
      :show-arrows="true"
      :show-dots="true"
      @button-click="handleSlideButtonClick"
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
          image: 'https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=1920&h=1080&fit=crop',
          title: 'Welcome to Our Platform',
          description: 'Discover amazing features and endless possibilities',
          buttonText: 'Get Started',
          action: 'signup'
        },
        {
          id: 2,
          image: 'https://images.unsplash.com/photo-1469474968028-56623f02e42e?w=1920&h=1080&fit=crop',
          title: 'Beautiful Design',
          description: 'Experience stunning visuals and smooth interactions',
          buttonText: 'Learn More',
          action: 'about'
        },
        {
          id: 3,
          image: 'https://images.unsplash.com/photo-1441974231531-c6227db76b6e?w=1920&h=1080&fit=crop',
          title: 'Join Our Community',
          description: 'Connect with thousands of users worldwide',
          buttonText: 'Sign Up Now',
          action: 'register'
        }
      ]
    };
  },
  methods: {
    handleSlideButtonClick(slide) {
      console.log('Button clicked on slide:', slide);
      // Handle button click based on slide action
      switch(slide.action) {
        case 'signup':
          // Navigate to signup page
          console.log('Navigate to signup');
          break;
        case 'about':
          // Navigate to about page
          console.log('Navigate to about');
          break;
        case 'register':
          // Navigate to register page
          console.log('Navigate to register');
          break;
      }
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

html, body, #app {
  width: 100%;
  height: 100vh;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
}
</style>
