<script setup lang="ts">
import { computed } from 'vue'
import { vIntersectionObserver } from '@vueuse/components'
import { useIntersectionAnimation } from '@/composables/intersectAnimation'
import { animateBackgroundIntersectionContacts } from '@/three/animations'

const contacts = [
  {
    name: 'email',
    link: 'xulixing322@gmail.com',
  },
]
const friends = [
  {
    name: 'G0J',
    link: 'https://baixie-g.github.io',
  },
]

const { animationProgress, animateIntersection } = useIntersectionAnimation()

const animationTranslateParagraph = computed(() => `${10 - animationProgress.value * 10}rem`)
const animationTranslateTitle = computed(() => `${5 - animationProgress.value * 5}rem`)

function onIntersection (entries: IntersectionObserverEntry[]) {
  animateIntersection(entries)

  const [{ isIntersecting }] = entries
  if (isIntersecting) {
    animateBackgroundIntersectionContacts()
  }
}
</script>

<template>
  <section
    v-intersection-observer="[onIntersection, { threshold: 0.5 }]"
    class="section-contacts"
  >
    <h2>Contact Me</h2>
    <ul class="contacts-list">
      <li
        v-for="contact in contacts"
        :key="contact.name"
      >
        <a
          class="btn-contact"
          :href="`mailto:${contact.link}`"
        >
          <svg
            t="1704549381974"
            class="icon"
            viewBox="0 0 1024 1024"
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
            p-id="3335"
            width="30"
            height="30"
          ><path
            d="M868.1 932H155.9c-77.4 0-140.3-62.9-140.3-140.3V232.3c0-77.4 63-140.3 140.3-140.3H868c77.4 0 140.3 62.9 140.3 140.3v559.4c0.1 77.4-62.9 140.3-140.2 140.3zM155.9 146.5c-47.3 0-85.8 38.5-85.8 85.8v559.4c0 47.3 38.5 85.8 85.8 85.8H868c47.3 0 85.7-38.5 85.7-85.8V232.3c0-47.3-38.5-85.8-85.7-85.8H155.9z"
            p-id="3336"
          /><path
            d="M511.9 557.7c-3.3 0-6.5-1-9.4-2.9l-467.6-326c-7.4-5.2-9.2-15.4-4.1-22.8 5.2-7.4 15.4-9.2 22.8-4.1l458.3 319.4L970.4 202c7.4-5.2 17.6-3.3 22.8 4.1 5.2 7.4 3.3 17.6-4.1 22.8L521.3 554.8a16.8 16.8 0 0 1-9.4 2.9z"
            p-id="3337"
          /></svg>
          <span> 给我写封邮件叭！ </span>
        </a>
      </li>
    </ul>
    <h2>My Friends</h2>
    <ul class="contacts-list">
      <li
        v-for="friend in friends"
        :key="friend.name"
      >
        <a
          class="btn-contact"
          :href="friend.link"
        >
          <span> {{ friend.name }} </span>
        </a>
      </li>
    </ul>
  </section>
</template>

<style scoped>
.section-contacts {
  /*margin: 20rem 0;*/
  height: 100vh;
}
.section-contacts > .contacts-list {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 0.5rem;
}

.contacts-list:hover {
  animation: bounce 1.2s ease
}

.section-contacts > * {
  opacity: v-bind(animationProgress);
  transform: translateY(v-bind(animationTranslateParagraph));
  max-width: 40rem;
}
.section-contacts > h2 {
  transform: translateY(v-bind(animationTranslateTitle));
  margin: 2rem 0;
}

@media (max-width: 800px) {
  .section-contacts > * {
    transform: translateY(calc(v-bind(animationTranslateParagraph) * var(--animation-values-coef)));
  }
  .section-contacts > h2 {
    transform: translateY(calc(v-bind(animationTranslateTitle) * var(--animation-values-coef)));
  }
}

.icon {
  vertical-align: bottom;
  margin-bottom: 3px;
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-30px);
  }
  60% {
    transform: translateY(-15px);
  }
}
</style>
