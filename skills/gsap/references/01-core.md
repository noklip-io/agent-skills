# GSAP Core API

## Tween Methods

### gsap.to()

Animates from current values TO specified values.

```javascript
// Basic
gsap.to('.box', { x: 200, duration: 1 })

// Multiple properties
gsap.to('.box', {
  x: 200,
  y: 100,
  rotation: 360,
  opacity: 0.5,
  duration: 2,
  ease: 'power2.inOut'
})

// Multiple targets
gsap.to(['.box1', '.box2', element], { x: 100 })
```

### gsap.from()

Animates FROM specified values to current values.

```javascript
// Fade in from below
gsap.from('.box', {
  opacity: 0,
  y: 50,
  duration: 1
})

// ⚠️ Renders immediately by default
// Set immediateRender: false if needed
gsap.from('.box', {
  y: -100,
  immediateRender: false
})
```

### gsap.fromTo()

Animates FROM specified values TO specified values.

```javascript
gsap.fromTo('.box',
  { opacity: 0, y: 50 },      // from
  { opacity: 1, y: 0, duration: 1 }  // to
)
```

### gsap.set()

Sets properties instantly (zero-duration tween).

```javascript
gsap.set('.box', { x: 100, opacity: 0 })

// Useful for initial states
gsap.set('.modal', { autoAlpha: 0 })
```

## Special Properties

### Timing

```javascript
gsap.to('.box', {
  x: 100,
  duration: 1,      // seconds (default: 0.5)
  delay: 0.5,       // delay before start
  repeat: 3,        // repeat count (-1 = infinite)
  repeatDelay: 0.5, // delay between repeats
  yoyo: true        // reverse on repeat
})
```

### Callbacks

```javascript
gsap.to('.box', {
  x: 100,
  onStart: () => console.log('Started'),
  onUpdate: () => console.log('Updated'),
  onComplete: () => console.log('Complete'),
  onRepeat: () => console.log('Repeated'),
  onReverseComplete: () => console.log('Reversed')
})

// With parameters
gsap.to('.box', {
  x: 100,
  onComplete: (msg) => console.log(msg),
  onCompleteParams: ['Animation done!']
})
```

### Control Options

```javascript
gsap.to('.box', {
  x: 100,
  paused: true,           // start paused
  reversed: true,         // start reversed
  overwrite: 'auto',      // kill conflicting tweens
  id: 'myTween',          // for gsap.getById()
  immediateRender: false  // don't render on creation
})
```

### CSS Properties

```javascript
gsap.to('.box', {
  // Transforms (GPU-accelerated)
  x: 100,           // translateX
  y: 50,            // translateY
  z: 0,             // translateZ (triggers 3D)
  xPercent: 50,     // translateX as percentage
  yPercent: -50,    // translateY as percentage
  rotation: 360,    // rotate in degrees
  rotationX: 45,    // 3D rotation
  rotationY: 45,
  scale: 1.5,
  scaleX: 2,
  scaleY: 0.5,
  skewX: 20,
  skewY: 10,
  transformOrigin: 'center center',

  // Standard CSS
  opacity: 0.5,
  width: 200,
  height: '50%',
  backgroundColor: '#ff0000',
  borderRadius: '50%',

  // Auto values
  autoAlpha: 0,     // opacity + visibility: hidden

  // Force 3D rendering
  force3D: true
})
```

### Relative Values

```javascript
gsap.to('.box', {
  x: '+=100',       // add 100 to current
  y: '-=50',        // subtract 50 from current
  rotation: '+=360' // add 360 degrees
})
```

### Function-Based Values

```javascript
gsap.to('.box', {
  x: (index, target, targets) => {
    return index * 100  // different value per target
  },
  duration: (i) => 0.5 + i * 0.1
})

// Random values
gsap.to('.box', {
  x: 'random(-200, 200)',
  y: 'random(-100, 100)',
  rotation: 'random(-180, 180)'
})

// Random from array
gsap.to('.box', {
  x: 'random([0, 100, 200, 300])'
})
```

## Tween Control Methods

```javascript
const tween = gsap.to('.box', { x: 100, duration: 2 })

// Playback
tween.play()
tween.pause()
tween.resume()
tween.reverse()
tween.restart()

// Position
tween.seek(1)           // jump to 1 second
tween.progress(0.5)     // jump to 50%
tween.time(0.5)         // set current time

// Speed
tween.timeScale(2)      // double speed
tween.timeScale(0.5)    // half speed

// State
tween.kill()            // destroy
tween.invalidate()      // clear recorded values
tween.revert()          // revert to pre-animation state

// Read state
console.log(tween.progress())   // 0-1
console.log(tween.isActive())   // boolean
console.log(tween.duration())   // total duration
```

## Global Methods

```javascript
// Kill tweens
gsap.killTweensOf('.box')
gsap.killTweensOf('.box', 'x,y')  // only x and y

// Get tweens
const tween = gsap.getById('myTween')
const tweens = gsap.getTweensOf('.box')

// Global pause/resume
gsap.globalTimeline.pause()
gsap.globalTimeline.resume()

// Defaults
gsap.defaults({
  ease: 'power2.out',
  duration: 1
})

// Configuration
gsap.config({
  autoSleep: 60,
  force3D: 'auto',
  nullTargetWarn: false
})
```

## Delayed Calls

```javascript
// Call function after delay
gsap.delayedCall(2, myFunction)
gsap.delayedCall(2, myFunction, [arg1, arg2])

// Kill delayed calls
gsap.killTweensOf(myFunction)
```

## Quick Setters

For performance-critical scenarios:

```javascript
// Create optimized setter
const setX = gsap.quickSetter('.box', 'x', 'px')
const setRotation = gsap.quickSetter('.box', 'rotation')

// Use in animation loop
gsap.ticker.add(() => {
  setX(mouseX)
  setRotation(angle)
})
```

## Match Media

Responsive animations:

```javascript
const mm = gsap.matchMedia()

mm.add('(min-width: 800px)', () => {
  // Desktop animations
  gsap.to('.box', { x: 500 })

  return () => {
    // Cleanup when condition no longer matches
  }
})

mm.add('(max-width: 799px)', () => {
  // Mobile animations
  gsap.to('.box', { x: 100 })
})

// Multiple conditions
mm.add({
  isDesktop: '(min-width: 800px)',
  isMobile: '(max-width: 799px)',
  reduceMotion: '(prefers-reduced-motion: reduce)'
}, (context) => {
  const { isDesktop, reduceMotion } = context.conditions

  if (reduceMotion) {
    gsap.set('.box', { x: 500 })
  } else if (isDesktop) {
    gsap.to('.box', { x: 500 })
  }
})
```
