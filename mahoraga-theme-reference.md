# Mahoraga Theme Reference

Design system extracted from [mahoraga.dev](https://mahoraga.dev/) - a clinical, warm-light theme for developer tools.

## Color Palette

### Backgrounds (warm off-whites)
```css
--cream: #fdfcfa;       /* primary background */
--subtle: #f5f3ef;      /* elevated surfaces */
```

### Text (warm grays)
```css
--muted: #9a9488;       /* secondary, hints */
--text: #3d3a35;        /* body text */
--bright: #1a1815;      /* headings, emphasis */
```

### Borders (warm gray range)
```css
--border: #e8e4dd;      /* subtle borders */
--border-dim: #d9d4cb;  /* stronger borders */
```

### Accents
```css
--accent: #2563eb;      /* primary blue */
--accent-dim: #1d4ed8;  /* hover/pressed state */
--success: #16a34a;     /* success/green */
--warning: #ca8a04;     /* warning/amber */
```

## Typography

```css
font-family: 'Iosevka Web', 'Iosevka', monospace;
font-size: 14px;
line-height: 1.6;
```

Technical emphasis via uppercase + letter-spacing:

```css
.technical-label {
  text-transform: uppercase;
  letter-spacing: 3px;
  font-size: 10px;
}
```

Font size scale: `10px` (labels) → `14px` (body) → `18px` (subheadings) → `24px` (logo/hero).

## Layout

```css
.container {
  max-width: 560px;
  margin: 0 auto;
  padding: 0 24px;
}
```

## Spacing Scale

```css
/* Base unit: 16px */
--space-sm: 16px;
--space-md: 20px;
--space-lg: 24px;
--space-xl: 56px;
--space-2xl: 64px;

/* Specific usage */
.container { padding: 0 24px; }
.section { margin-bottom: 56px; }
.card { padding: 20px; }
```

## Animations

### Clunky Rotation (signature animation)
```css
@keyframes clunkRotate {
  0%   { transform: rotate(0deg); }
  12%  { transform: rotate(45deg); }
  25%  { transform: rotate(90deg); }
  37%  { transform: rotate(135deg); }
  50%  { transform: rotate(180deg); }
  62%  { transform: rotate(225deg); }
  75%  { transform: rotate(270deg); }
  87%  { transform: rotate(315deg); }
  100% { transform: rotate(360deg); }
}

.rotating-logo {
  animation: clunkRotate 26s steps(1) infinite;
}
```

### Fade-in Cascade
```css
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

.fade-in {
  animation: fadeIn 0.8s ease-out forwards;
}

/* Stagger children */
.fade-in:nth-child(1) { animation-delay: 0.1s; }
.fade-in:nth-child(2) { animation-delay: 0.2s; }
.fade-in:nth-child(3) { animation-delay: 0.3s; }
.fade-in:nth-child(4) { animation-delay: 0.4s; }
.fade-in:nth-child(5) { animation-delay: 0.5s; }
.fade-in:nth-child(6) { animation-delay: 0.6s; }
```

### Component Transitions
```css
/* FAQ toggle expand/collapse */
.faq-content {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.3s ease;
}
.faq-content.open {
  max-height: 500px;
}

/* Copy button icon swap */
.copy-icon {
  transition: transform 0.15s ease;
}
.copy-icon:active {
  transform: scale(0.9);
}
```

## Interactive Components

### FAQ Accordion
```css
.faq-toggle {
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
}

.faq-icon {
  transition: transform 0.2s ease;
}
.faq-toggle[aria-expanded="true"] .faq-icon {
  transform: rotate(45deg);
}
```

### Copy Button
```css
.copy-btn {
  background: transparent;
  border: 1px solid var(--border);
  padding: 8px 12px;
  cursor: pointer;
  transition: border-color 0.15s;
}
.copy-btn:hover {
  border-color: var(--border-dim);
}
```

## Hover States

```css
/* Standard link: muted → text */
a {
  color: var(--muted);
  transition: color 0.15s;
}
a:hover {
  color: var(--text);
}

/* Accent link: accent → accent-dim */
a.primary {
  color: var(--accent);
  transition: color 0.15s;
}
a.primary:hover {
  color: var(--accent-dim);
}
```

## Border Radius & Shadows

Minimal. Sharp corners preferred, subtle radius on buttons:

```css
.btn { border-radius: 4px; }
.card { border-radius: 0; }
```

No shadows - relies on borders and background contrast.

## Tailwind Config (if using Tailwind)

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        // Backgrounds
        cream: '#fdfcfa',
        subtle: '#f5f3ef',
        // Text
        muted: '#9a9488',
        text: '#3d3a35',
        bright: '#1a1815',
        // Borders
        border: {
          DEFAULT: '#e8e4dd',
          dim: '#d9d4cb',
        },
        // Accents
        accent: {
          DEFAULT: '#2563eb',
          dim: '#1d4ed8',
        },
        success: '#16a34a',
        warning: '#ca8a04',
      },
      fontFamily: {
        mono: ['Iosevka Web', 'Iosevka', 'JetBrains Mono', 'monospace'],
      },
      maxWidth: {
        content: '560px',
      },
    },
  },
}
```

## Example Usage

```html
<body style="background: var(--cream); color: var(--text);">
  <main class="container">
    <h1 style="color: var(--bright);">MAHORAGA</h1>
    <p style="color: var(--muted);">AI trading strategies</p>
    <a href="#" style="color: var(--accent);">Get started</a>
  </main>
</body>
```

## Interactive Logo

The logo rotation is clickable - pauses animation and manually increments 45° per click. Creates tactile, mechanical feedback.

```css
.logo {
  cursor: pointer;
  transition: transform 0.1s steps(1);
}

.logo.paused {
  animation-play-state: paused;
}
```

```js
// Click to pause + increment
logo.addEventListener('click', () => {
  rotationStep += 45;
  logo.style.transform = `rotate(${rotationStep}deg)`;
  logo.classList.add('paused');
});
```

## Copy Button States

Dual-icon pattern with success confirmation:

```css
.copy-btn {
  position: relative;
}

.copy-icon, .check-icon {
  transition: opacity 0.15s, transform 0.15s;
}

.copy-btn.copied .copy-icon {
  opacity: 0;
  transform: scale(0.8);
}

.copy-btn.copied .check-icon {
  opacity: 1;
  color: var(--success);
}
```

## Brand Voice & UX Philosophy

### Risk-First Tone
Disclaimers integrated into UX, not hidden in footer:

```html
<!-- Prominent warning box -->
<div class="warning-box">
  Paper trading only. Educational purposes.
</div>
```

- Qualifying language appears inline, not as legal afterthought
- "Responsible defaults over hype"
- Warnings are part of the design, not fighting against it

### Builder Over Trader
- Terminal commands (`$ git clone`) emphasized over GUI
- Dashboard exists but is visually understated
- Technical control > polished broker aesthetic
- Appeals to devs who want to customize, not retail traders

### Copy Style
- Direct, instructional
- Step-by-step numbered lists
- No marketing fluff or urgency
- Calm confidence, not hype

## Key Design Principles

1. **Warm off-whites** - `#fdfcfa` not sterile white; reduces eye strain
2. **Blue accent** - trustworthy, professional `#2563eb` against warm neutrals
3. **Monospace everything** - Iosevka reinforces technical credibility
4. **Deliberate motion** - slow 26s rotation + staggered fades feel intentional, not flashy
5. **Clinical minimalism** - clarity over decoration; no noise/grain
6. **Narrow container** - 560px keeps focus tight
7. **Uppercase labels** - wide letter-spacing (3-4px) for technical emphasis
8. **Tactile interactions** - clickable logo, clear copy feedback; mechanical not slick
9. **Risk-aware UX** - disclaimers as design elements, not legal afterthoughts
10. **Builder-first hierarchy** - code/CLI primary, dashboards secondary
