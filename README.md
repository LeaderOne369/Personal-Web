# Personal Portfolio Website

[![Vue](https://img.shields.io/badge/Vue-3.4.5-4FC08D?style=flat-square&logo=vue.js)](https://vuejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.1.6-3178C6?style=flat-square&logo=typescript)](https://www.typescriptlang.org/)
[![Three.js](https://img.shields.io/badge/Three.js-0.149.0-049EF4?style=flat-square&logo=three.js)](https://threejs.org/)
[![Vite](https://img.shields.io/badge/Vite-4.4.2-646CFF?style=flat-square&logo=vite)](https://vitejs.dev/)
[![GitHub](https://img.shields.io/badge/GitHub-Profile-181717?style=flat-square&logo=github)](https://github.com/LeaderOne369?tab=repositories)

A modern, interactive personal portfolio website built with Vue 3, TypeScript, and Three.js, featuring 3D animations, responsive design, and real-time danmaku messaging system.

## 🚀 Live Demo

Visit the live website: [Personal Portfolio](https://leaderone369.github.io/) _(deployed via GitHub Pages)_

## 📋 Overview

This project showcases my journey as a Software Engineering student at Hefei University of Technology, highlighting my technical skills, project experiences, and professional development. The website serves as both a personal brand platform and a demonstration of modern web development capabilities.

### 🎯 Key Features

- **3D Interactive Background**: Custom Three.js scene with dynamic particle systems and smooth animations
- **Responsive Design**: Fully responsive layout optimized for desktop, tablet, and mobile devices
- **Smooth Animations**: GSAP-powered transitions and scroll-triggered animations
- **Real-time Danmaku**: Interactive messaging system with persistent storage
- **Intersection Observer**: Performance-optimized animations triggered by viewport visibility
- **Modern UI/UX**: Clean, minimalist design with intuitive navigation

## 🛠️ Tech Stack

### Frontend Framework

- **Vue 3** - Progressive JavaScript framework with Composition API
- **TypeScript** - Type-safe JavaScript for better development experience
- **Vite** - Fast build tool and development server

### 3D & Animations

- **Three.js** - 3D graphics library for WebGL rendering
- **GSAP** - High-performance animation library
- **@vueuse/core** - Vue composition utilities

### UI & Styling

- **Tailwind CSS** - Utility-first CSS framework
- **PostCSS** - CSS processing tool with Autoprefixer

### Additional Libraries

- **danmaku-vue** - Real-time danmaku (bullet screen) component
- **vite-ssg** - Static Site Generation for better SEO and performance

## 📁 Project Structure

```
src/
├── components/           # Vue components
│   ├── BackgroundScene.vue    # 3D background canvas
│   ├── SectionAbout.vue       # Personal introduction
│   ├── SectionExperience.vue  # Professional experience
│   ├── SectionContacts.vue    # Contact information
│   └── SectionTitle.vue       # Landing page title
├── three/               # Three.js related files
│   ├── index.ts         # Main 3D scene setup
│   ├── animations.ts    # Animation controls
│   └── glsl/            # GLSL shaders
├── composables/         # Vue composables
│   ├── intersectAnimation.ts  # Intersection observer logic
│   └── timePassed.ts           # Time calculation utilities
├── assets/              # Static assets
│   ├── css/             # Stylesheets
│   ├── fonts/           # Custom fonts
│   └── loading.gif      # Loading animation
└── main.ts              # Application entry point
```

## 🚀 Quick Start

### Prerequisites

- Node.js 18+
- pnpm (recommended) or npm

### Installation

```bash
# Clone the repository
git clone https://github.com/LeaderOne369/personal-web.git
cd personal-web

# Install dependencies
pnpm install

# Start development server
pnpm run dev

# Build for production
pnpm run build

# Preview production build
pnpm run preview
```

The development server will start at `http://localhost:3333`.

## 🎨 Features in Detail

### 3D Background System

- Custom particle systems with dynamic movement
- WebGL-accelerated rendering
- Responsive to user interactions and scroll events

### Experience Timeline

- Chronological display of academic and professional milestones
- Smooth scroll animations with intersection observers
- Comprehensive showcase of technical projects and achievements

### Interactive Elements

- **Danmaku System**: Real-time messaging with local storage persistence
- **Navigation Sidebar**: Smooth scrolling to different sections
- **Responsive Animations**: GPU-accelerated transitions

## 📊 Performance Optimizations

- **Lazy Loading**: Components loaded on demand
- **Intersection Observer**: Animations triggered only when visible
- **Static Site Generation**: Pre-rendered pages for better SEO
- **Asset Optimization**: Compressed images and minified bundles

## 🎓 Academic & Professional Background

### Education

- **Hefei University of Technology** (2022 - Present)
  - Bachelor of Software Engineering
  - GPA: 3.90/4.3
  - Relevant Coursework: Data Structures, Algorithms, Software Engineering, Web Development

### Key Projects

1. **OTC Project Management System** (Java Training, 2024)

   - Team leadership and full-stack development
   - Technologies: Java, Spring Boot, MySQL

2. **Knowledge Sharing Platform** (Software Engineering Training, 2025)

   - System architecture design and implementation
   - Technologies: Vue.js, Node.js, MongoDB

3. **Smart Hospital Customer Service System** (Enterprise Training, 2025)
   - Enterprise-level application development
   - Technologies: React/Vue, Microservices, Docker

### Professional Experience

- **IAV GmbH Shanghai R&D Center** (2025.10 - Present)
  - Software Development Engineer Intern
  - VENAS Engine: Autonomous driving test and data analysis platform

### Certifications & Scores

- **TOEFL**: 110 (2025.08)
- **GRE**: 331 (Quantitative: Full Score, 2025.09)

## 🤝 Contact Information

- **Email**: xulixing322@gmail.com
- **GitHub**: [https://github.com/LeaderOne369?tab=repositories](https://github.com/LeaderOne369?tab=repositories)
- **LinkedIn**: [Your LinkedIn Profile]

## 📝 Development Notes

This project was developed as part of my portfolio for graduate school applications. It demonstrates:

- Proficiency in modern JavaScript/TypeScript development
- Understanding of 3D graphics and WebGL programming
- Experience with Vue.js ecosystem and component architecture
- Knowledge of build tools, deployment, and performance optimization
- Ability to create engaging user interfaces and interactions

## 🔧 Build & Deployment

### Development

```bash
pnpm run dev          # Start dev server
pnpm run type-check   # TypeScript type checking
```

### Production

```bash
pnpm run build        # Build for production
pnpm run preview      # Preview production build
```

### Deployment

The site is configured for static hosting and can be deployed to:

- GitHub Pages
- Netlify
- Vercel
- Any static web server

## 📄 License

This project is private and intended for personal use only.

## 🙏 Acknowledgments

- Vue.js team for the excellent framework
- Three.js community for 3D graphics inspiration
- GSAP for animation capabilities
- All open-source contributors whose work made this project possible

---

_Built with ❤️ by Xu Lixing | Last updated: November 2025_
