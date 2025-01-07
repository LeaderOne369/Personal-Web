<script setup lang="ts">
import { computed, ref } from 'vue'
import { vIntersectionObserver } from '@vueuse/components'
import { useIntersectionAnimation } from '@/composables/intersectAnimation'
import { useTimePassed } from '@/composables/timePassed'
import { animateBackgroundIntersectionAbout } from '@/three/animations'

const myName = '徐力行'

const { years: age } = useTimePassed('2003-11-24T05:00:00+0500')
const { sumSeconds } = useTimePassed('2024-01-06T15:00:00+0500')

const onlySeconds = ref(true)
const changeExpTime = () => onlySeconds.value = !onlySeconds.value

const { animationProgress, animateIntersection } = useIntersectionAnimation()

const animationTranslateParagraph = computed(() => `${10 - animationProgress.value * 10}rem`)
const animationTranslateTitle = computed(() => `${5 - animationProgress.value * 5}rem`)

function onIntersection (entries: IntersectionObserverEntry[]) {
  animateIntersection(entries)

  const [{ isIntersecting }] = entries
  if (isIntersecting) {
    animateBackgroundIntersectionAbout()
  }
}
</script>

<template>
  <section
    v-intersection-observer="[onIntersection, { threshold: 0.5 }]"
    class="section-about"
  >
    <h2>About Me</h2>
    <div class="about-content">
      <div class="text-content">
        <p>
          旅行者你好！欢迎来到我的个人网站。我是软件一班的{{ myName }}，
          一名 <span>{{ age }}</span> 岁的学生。
          我喜欢编程、听音乐和打游戏。我的理想是每天都比过往变得更好。本网站已经完成
          <span
            v-if="onlySeconds"
            class="exp-time"
            @click="changeExpTime"
          >
            {{ sumSeconds }} 秒.
          </span>
        </p>
      </div>
      <div>
        <div
          class="profile-picture"
        />
      </div>
    </div>
  </section>
</template>

<style scoped>
.section-about {
  margin-bottom: 20rem;
}

.section-about > .content-about > p {
  opacity: v-bind(animationProgress);
  transform: translateY(v-bind(animationTranslateParagraph));
}
.section-about > h2 {
  transform: translateY(v-bind(animationTranslateTitle));
  margin: 2rem 0;
}

.exp-time {
  cursor: pointer;
  color: var(--color-text-highlight);
}

@media (max-width: 800px) {
  .section-about {
    margin-bottom: 10rem;
  }
  .section-about > * {
    transform: translateY(calc(v-bind(animationTranslateParagraph) * var(--animation-values-coef)));
  }
  .section-about > h2 {
    transform: translateY(calc(v-bind(animationTranslateTitle) * var(--animation-values-coef)));
  }
}

.about-content {
  display: flex;
  align-items: flex-start;
}

.text-content {
  max-width: 40rem;
}

.profile-picture {
  width: 20rem;
  height: 20rem;
  border-radius: 50%;
  background: url("https://s1.imagehub.cc/images/2024/01/07/70b34d484aa53c861681517930d46081.jpeg") center center/cover no-repeat;
  margin-left: 10rem; 
  margin-top: -8rem;
  transition: transform 0.3s ease-out;
}

.profile-picture:hover {
  transform: scale(1.2);
  transition: transform 0.4s ease;
}

.profile-picture::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border: 4px solid transparent;
  border-radius: 50%;
  box-shadow: 0 0 20px rgba(255, 255, 255, 0.8); 
  opacity: 0;
  transition: opacity 0.3s ease-out;
}

.profile-picture:hover::before {
  opacity: 1;
}
</style>
