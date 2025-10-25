# Hero Banner Component

A responsive and customizable Hero Banner component for Vue.js applications.

## Features

- Customizable title and subtitle
- Background image or solid color support
- Adjustable height
- Optional overlay for better text readability
- Slot support for call-to-action buttons
- Fully responsive design
- Clean and modern styling

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `title` | String | 'Welcome to Our Site' | Main heading text |
| `subtitle` | String | 'Discover amazing content and experiences' | Subtitle text |
| `backgroundImage` | String | '' | URL for background image |
| `backgroundColor` | String | '#667eea' | Background color (used if no image) |
| `height` | String | '500px' | Banner height |
| `overlay` | Boolean | true | Show dark overlay for better text contrast |

## Usage

### Basic Usage

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

### With Background Image

```vue
<HeroBanner
  title="Explore the World"
  subtitle="Your adventure starts here"
  background-image="https://example.com/hero-image.jpg"
  height="600px"
/>
```

### With Call-to-Action Buttons

```vue
<HeroBanner
  title="Get Started Today"
  subtitle="Join thousands of satisfied customers"
>
  <button class="btn-primary">Sign Up</button>
  <button class="btn-secondary">Learn More</button>
</HeroBanner>
```

### Custom Background Color

```vue
<HeroBanner
  title="Custom Style"
  subtitle="With your brand colors"
  background-color="#ff6b6b"
  :overlay="false"
/>
```

## Customization

The component uses scoped styles, but you can override them by using deeper selectors or by modifying the component styles directly.

## Browser Support

Works with all modern browsers that support Vue.js 3.x.
