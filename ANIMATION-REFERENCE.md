# 🎨 RouteIQ Animation Reference - Quick Start Guide

## 📋 File Locations

```
projectRoot/
├── src/components/
│   ├── MapView.jsx          ← Real-time animated map
│   ├── Dashboard.jsx         ← Staggered card animations
│   └── RouteForm.jsx         ← Input & button animations
├── routeiq.html             ← All CSS animations (25+ keyframes)
├── ENHANCEMENTS.md          ← Full feature documentation
└── ANIMATION-GUIDE.md       ← Visual animation flows
```

---

## 🎬 Using Animations in Components

### 1. **Staggered Grid Items** (Dashboard)
```jsx
import { useState } from 'react';

function BentoItem({ children, delay = 0, className = '' }) {
  return (
    <div 
      className={`glass-card bento-item ${className}`}
      style={{
        animation: `fadeUpScale 0.6s cubic-bezier(0.16,1,0.3,1) forwards`,
        animationDelay: `${delay}ms`,
        opacity: 0,
      }}
    >
      {children}
    </div>
  );
}

// Usage:
<BentoItem delay={0}>Safety Score</BentoItem>
<BentoItem delay={80}>ETA</BentoItem>
<BentoItem delay={160}>AI Insights</BentoItem>
```

### 2. **Real-Time Pulse Indicator**
```jsx
// In JSX:
<span className="live-pulse">●</span> 95% Confidence

// CSS:
.live-pulse {
  display: inline-block;
  animation: livePulse 2s cubic-bezier(0.4, 0.0, 0.6, 1) infinite;
  margin-right: 4px;
  color: #818CF8;
}
```

### 3. **Animated Number Counter**
```jsx
function AnimatedNumber({ value, duration = 1200 }) {
  const [display, setDisplay] = useState(0);
  
  useEffect(() => {
    let start = null;
    const animate = (ts) => {
      if (!start) start = ts;
      const p = Math.min((ts - start) / duration, 1);
      const ease = 1 - Math.pow(1 - p, 4);
      setDisplay(Math.round(value * ease));
      if (p < 1) requestAnimationFrame(animate);
    };
    requestAnimationFrame(animate);
  }, [value, duration]);
  
  return <>{display}</>;
}

// Usage:
<AnimatedNumber value={42} duration={1200} />
```

### 4. **Vehicle Position Animation** (Map)
```jsx
useEffect(() => {
  const animate = () => {
    const elapsed = Date.now() - startTime;
    const progress = (elapsed % duration) / duration;
    
    // Interpolate position along path
    const index = Math.floor(progress * (path.length - 1));
    const current = path[index];
    const next = path[index + 1];
    const localProg = (progress * (path.length - 1)) - index;
    
    const interpolated = {
      lat: current.lat + (next.lat - current.lat) * localProg,
      lng: current.lng + (next.lng - current.lng) * localProg,
    };
    
    setVehiclePos(interpolated);
    requestAnimationFrame(animate);
  };
  
  requestAnimationFrame(animate);
}, []);
```

---

## 🎨 CSS Animation Classes

### Fade & Scale Animations
```css
/* Fade up with scale - used for grid items */
.bento-item {
  animation: fadeUpScale 0.6s cubic-bezier(0.16,1,0.3,1) forwards;
}

/* Simple fade up - used for sections */
.fade-up {
  animation: fadeUp 0.6s cubic-bezier(0.22, 1, 0.36, 1) forwards;
}

/* Cascade in - used for lists */
.incident-item {
  animation: cascadeIn 0.5s cubic-bezier(0.22, 1, 0.36, 1) both;
}
```

### Real-Time Indicators
```css
/* Pulsing live indicator */
.live-pulse {
  animation: livePulse 2s cubic-bezier(0.4, 0.0, 0.6, 1) infinite;
}

/* Badge pulse for notifications */
.badge-live {
  animation: badgePulse 2s infinite;
}

/* Sync indicator pulse */
.sync-indicator {
  animation: syncPulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
```

### Loading & Transitions
```css
/* Shimmer effect for loading */
.shimmer-load {
  animation: shimmer 2s infinite;
}

/* Map ready blur to clear */
.map-wrapper--ready {
  animation: mapReady 0.8s cubic-bezier(0.22, 1, 0.36, 1) forwards;
}

/* Data flowing animation */
.data-flowing {
  animation: dataFlow 3s ease-in-out infinite;
}
```

### Interactive Animations
```css
/* Button press effect */
.btn:active {
  animation: buttonPress 0.4s cubic-bezier(0.22, 1, 0.36, 1);
}

/* Glow effect on hover */
.glow-active {
  animation: glow 2s ease-in-out infinite;
}

/* Tooltip fade */
.tooltip {
  animation: tooltipFade 0.3s cubic-bezier(0.22, 1, 0.36, 1) forwards;
}
```

---

## ⏱️ Animation Timing Reference

| Duration | Use Case | Example |
|----------|----------|---------|
| **300ms** | Quick feedback, micro-interactions | Button hover, input focus |
| **600ms** | Standard transition, grid item | Card enter, fade effects |
| **800ms** | Noticeable entrance, map load | Dashboard reveal, blur to clear |
| **1200ms** | Number animations | Counter tick-up, progress fill |
| **2000ms** | Real-time pulses | Live indicator, sync pulse |
| **12000ms** | Continuous loops | Vehicle animation, data flow |

---

## 🎯 Easing Curves

### Primary Easing (Most Used)
```css
cubic-bezier(0.22, 1, 0.36, 1)  /* Spring-like, bouncy */
```

### Smooth Easing
```css
cubic-bezier(0.16, 1, 0.3, 1)   /* Less bounce */
```

### Linear (Continuous)
```css
linear                           /* Vehicle, data flow */
```

### Elastic Easing
```css
cubic-bezier(0.34, 1.56, 0.64, 1) /* Overshoot for fills */
```

---

## 🛠️ Common Customizations

### Change Animation Speed
```jsx
// In component props:
<BentoItem delay={0} />  // 0ms delay

// In CSS:
animation: fadeUpScale 0.6s ...  // Change 0.6s to your duration
```

### Change Animation Color
```jsx
// In MapView:
const hotspotColor = intensity > 0.6 ? '#EF4444' : '#F59E0B';

// In Dashboard:
const scoreColor = score >= 75 ? '#10B981' : '#EF4444';
```

### Add Additional Animation
```css
@keyframes yourAnimation {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.your-element {
  animation: yourAnimation 0.6s cubic-bezier(0.22, 1, 0.36, 1) forwards;
}
```

---

## 🚨 Disable Animations (Accessibility)

```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 🔍 Debugging Animations

### Slow Down Animations (DevTools)
```javascript
// In browser console:
document.documentElement.style.setProperty('--animation-duration', '3s');

// Or CSS variable:
:root {
  --animation-duration: 0.6s;
}

.bento-item {
  animation-duration: var(--animation-duration);
}
```

### View Animation Performance
```javascript
// Chrome DevTools > Animations panel
// Shows all active animations and allows playback control
```

---

## 📱 Mobile Optimization

### Touch-Friendly Timing
```css
@media (max-width: 768px) {
  .bento-item {
    animation-duration: 0.4s;  /* Faster on mobile */
  }
}
```

### Reduce Motion Support
```css
@media (prefers-reduced-motion: reduce) {
  .bento-item {
    animation: none;
    opacity: 1;
    transform: none;
  }
}
```

---

## 🎬 Advanced: RAF Animation Loop

```jsx
// For continuous smooth animations like vehicle tracking
useEffect(() => {
  let animationId;
  let startTime = Date.now();
  
  const animate = () => {
    const elapsed = Date.now() - startTime;
    const progress = (elapsed % duration) / duration;
    
    // Update state based on progress
    setPosition(calculatePosition(progress));
    
    animationId = requestAnimationFrame(animate);
  };
  
  animationId = requestAnimationFrame(animate);
  
  return () => cancelAnimationFrame(animationId);
}, []);
```

---

## 📊 Performance Tips

1. **Use transform & opacity**: GPU-accelerated, smooth
   ```css
   transform: translateY(0) scale(1);  /* ✅ Good */
   top: 0; left: 0;                   /* ❌ Bad */
   ```

2. **Use will-change sparingly**:
   ```css
   .animated-item {
     will-change: transform, opacity;
   }
   ```

3. **Batch animations**: Use CSS instead of JS when possible

4. **Use RequestAnimationFrame** for custom animations:
   ```javascript
   requestAnimationFrame(updateFrame);  // 60fps sync
   ```

---

## ✅ Testing Animations

```jsx
// Test animation timing
<BentoItem delay={80}>Item</BentoItem>
// Should appear 80ms after previous

// Test real-time pulse
<span className="live-pulse">●</span>
// Should pulse smoothly every 2s

// Test vehicle animation
// Vehicle should smoothly move along route in 12s cycle
```

---

## 📚 Further Reading

- CSS Animations: [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations)
- RequestAnimationFrame: [MDN Docs](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame)
- Easing Functions: [easings.net](https://easings.net/)

---

**Version**: 2.0  
**Last Updated**: April 15, 2026  
**Status**: Production Ready ✨
