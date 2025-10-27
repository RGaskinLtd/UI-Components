# Hero Slider Component (V2)

A beautiful, responsive Vue.js hero slider component with smooth transitions, autoplay functionality, and intuitive navigation controls.

## Notion Page ID
**295e3dc7-a2e1-8079-ae5d-cefdb8df4d6e**

## Features

- Smooth slide transitions with fade and slide effects
- Autoplay functionality with configurable intervals
- Navigation arrows for manual control
- Dot indicators for quick navigation
- Responsive design for mobile and desktop
- Customizable slide content (title, description, button)
- Event emission for button clicks
- Accessible controls with ARIA labels
- Beautiful overlay effects and animations

## Installation

1. Copy the `HeroSlider.vue` component to your Vue.js project
2. Import and register the component in your parent component

## Usage

```vue
<template>
  <HeroSlider
    :slides="heroSlides"
    :autoplay="true"
    :interval="5000"
    @button-click="handleButtonClick"
  />
</template>

<script>
import HeroSlider from './HeroSlider.vue';

export default {
  components: {
    HeroSlider
  },
  data() {
    return {
      heroSlides: [
        {
          id: 1,
          title: 'Welcome to Our Amazing Product',
          description: 'Discover the future of innovation',
          image: 'https://example.com/image1.jpg',
          buttonText: 'Get Started',
          link: '/get-started'
        },
        {
          id: 2,
          title: 'Build Something Great',
          description: 'Transform your ideas into reality',
          image: 'https://example.com/image2.jpg',
          buttonText: 'Learn More',
          link: '/learn-more'
        }
      ]
    };
  },
  methods: {
    handleButtonClick(slide) {
      console.log('Button clicked:', slide);
      // Handle navigation or custom actions
    }
  }
};
</script>
```

## Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `slides` | Array | Yes | - | Array of slide objects (see structure below) |
| `autoplay` | Boolean | No | `true` | Enable/disable automatic slide transitions |
| `interval` | Number | No | `5000` | Time in milliseconds between slide transitions |

## Slide Object Structure

Each slide object should have the following properties:

```javascript
{
  id: Number or String (required),
  title: String (required),
  description: String (optional),
  image: String (required) - URL to background image,
  buttonText: String (optional),
  link: String (optional) - for your navigation logic
}
```

## Events

| Event | Payload | Description |
|-------|---------|-------------|
| `button-click` | `slide` object | Emitted when a slide button is clicked |

## Customization

### Styling

The component uses scoped styles that can be customized by modifying the `<style>` section in `HeroSlider.vue`. Key customization areas:

- Colors and backgrounds
- Animation timing and effects
- Button styles and hover effects
- Responsive breakpoints
- Overlay opacity

### Transition Effects

Modify the `.slide-enter-active` and `.slide-leave-active` classes to change transition effects.

## Browser Support

- Modern browsers (Chrome, Firefox, Safari, Edge)
- Supports responsive design for mobile devices
- Uses CSS Grid and Flexbox for layout

## License

MIT

## Contributing

Feel free to submit issues and enhancement requests!
