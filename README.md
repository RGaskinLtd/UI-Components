# UI Components

A collection of reusable Vue.js UI components.

## Components

### Hero Banner Component

A responsive and customizable Hero Banner component for Vue.js applications.

#### Features

- Customizable title and subtitle
- Background image or solid color support
- Adjustable height
- Optional overlay for better text readability
- Slot support for call-to-action buttons
- Fully responsive design
- Clean and modern styling

#### Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `title` | String | 'Welcome to Our Site' | Main heading text |
| `subtitle` | String | 'Discover amazing content and experiences' | Subtitle text |
| `backgroundImage` | String | '' | URL for background image |
| `backgroundColor` | String | '#667eea' | Background color (used if no image) |
| `height` | String | '500px' | Banner height |
| `overlay` | Boolean | true | Show dark overlay for better text contrast |

#### Usage

##### Basic Usage

```vue
<template>
  <HeroBanner
    title="Welcome to My Site"
    subtitle="Building amazing experiences"
  />
</template>

<script>
import HeroBanner from './HeroBanner.vue'

export default {
  components: {
    HeroBanner
  }
}
</script>
```

##### With Background Image

```vue
<HeroBanner
  title="Explore the World"
  subtitle="Your adventure starts here"
  background-image="https://example.com/hero-image.jpg"
  height="600px"
/>
```

##### With Call-to-Action Buttons

```vue
<HeroBanner
  title="Get Started Today"
  subtitle="Join thousands of satisfied customers"
>
  <button class="btn-primary">Sign Up</button>
  <button class="btn-secondary">Learn More</button>
</HeroBanner>
```

---

### Hero Slider Component

A beautiful, responsive Vue.js hero slider component with smooth transitions, autoplay, navigation arrows, and dot indicators.

#### Features

- Smooth slide transitions with fade effects
- Autoplay functionality with customizable speed
- Navigation arrows for manual slide control
- Dot indicators for quick navigation
- Fully responsive design
- Customizable content (title, description, button)
- Event emission for button clicks
- Keyboard navigation support
- Touch-friendly interface

#### Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `slides` | Array | Yes | - | Array of slide objects |
| `autoplay` | Boolean | No | `true` | Enable/disable automatic slide transitions |
| `autoplaySpeed` | Number | No | `5000` | Time in milliseconds between slide transitions |
| `showArrows` | Boolean | No | `true` | Show/hide navigation arrows |
| `showDots` | Boolean | No | `true` | Show/hide dot indicators |

#### Usage

```vue
<template>
  <HeroSlider
    :slides="heroSlides"
    :autoplay="true"
    :autoplay-speed="5000"
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
          image: 'path/to/image1.jpg',
          title: 'Welcome to Our Platform',
          description: 'Discover amazing features',
          buttonText: 'Get Started'
        }
      ]
    };
  }
};
</script>
```

---

## Browser Support

All components work with modern browsers that support Vue.js 3.x.

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
