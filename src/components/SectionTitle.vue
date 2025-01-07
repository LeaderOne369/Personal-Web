<script setup lang="ts">
import IconLess from '@/components/IconLess.vue'
import { computed, ref } from 'vue'
import { animate } from 'popmotion'
import { vIntersectionObserver } from '@vueuse/components'
import { animateBackgroundIntersectionTitle } from '@/three/animations'

const NAME = [
  { letter: '我', id: 7 },
  { letter: '的', id: 8 },
  { letter: '网', id: 0 },
  { letter: '站', id: 1 },
  { letter: '开', id: 2 },
  { letter: '发', id: 9 },
  { letter: '大', id: 999 },
  { letter: '作', id: 10 },
  { letter: '业', id: 11 },
  { letter: '~', id: 12 },
  ]

const NICKNAME = [
  { letter: '祝', id: 10 },
  { letter: '你', id: 11 },
  { letter: '天', id: 3 },
  { letter: '天', id: 3 },
  { letter: '开', id: 3 },
  { letter: '心', id: 3 },
  { letter: '!', id: 7 },

]

const isName = ref(false)
const name = computed(() => isName.value ? NAME : NICKNAME)

function onIntersection ([{ isIntersecting }]: IntersectionObserverEntry[]) {
  isName.value = isIntersecting

  if (isIntersecting) {
    animateBackgroundIntersectionTitle()
  }
}

function onBeforeEnter (el: Element) {
  const elem = el as HTMLElement
  elem.style.transform = 'translateY(1em) translateX(0.5em) rotateX(90deg)'
}

function onEnter (el: Element, done: () => void) {
  const elem = el as HTMLElement
  animate({
    from: 0,
    to: 100,
    type: 'spring',
    stiffness: 180,
    damping: 20,
    elapsed: -15 * +(elem.dataset.index ?? 0),
    onUpdate: latest => elem.style.transform = `
      translateY(${-latest / 100 * 1 + 1}em) 
      translateX(${-latest / 100 * 0.5 + 0.5}em) 
      rotateX(${-latest / 100 * 90 + 90}deg)`,
    onComplete: done,
  })
}

function onLeave (el: Element, done: () => void) {
  const elem = el as HTMLElement
  elem.style.opacity = '0'
  done()
}
</script>

<template>
  <section
    v-intersection-observer="[onIntersection, { threshold: 0.8 }]"
    class="section-title"
  >
    <div class="title">
      <TransitionGroup
        name="name"
        tag="h1"
        @before-enter="onBeforeEnter"
        @enter="onEnter"
        @leave="onLeave"
      >
        <span
          v-for="(letter, index) in name"
          :key="letter.id"
          :data-index="index"
          :class="{
            'surname-start': letter.id === 999,
            'sennery': ![0, 1, 2].includes(letter.id) && !isName,
          }"
        >
          {{ letter.letter }}
        </span>
      </TransitionGroup>
      <span
        class="spec"
        :class="{ active: isName }"
      >
        {{ }}
      </span>

      <div
        v-if="isName"
        class="hint"
      >
        <IconLess />
        <span class="scroll-text">scroll down</span>
        <span class="swipe-text">swipe up</span>
      </div>
    </div>
    <div class="info-lines">
      <div class="info-line">班级：<span class="larger-text">软件22-1班</span></div>
      <div class="info-line">姓名：<span class="larger-text">徐力行</span></div>
      <div class="info-line">学号：<span class="larger-text">2022213386</span></div>
    </div>
    
  </section>
</template>

<style scoped>
.section-title {
  height: 100vh;
}
.info-lines {
  font-size: 1.5rem; /* 根据需要调整字体大小 */
}

.section-title > .title > h1 {
  display: flex;
}
.section-title > .title > h1 > span {
  transform-origin: 0 0;
}

.surname-start {
  padding-left: 1.5rem;
}
.sennery {
  color: var(--color-text-highlight);
}

.name-move, .spec.active {
  transition: all 0.6s cubic-bezier(0, 1, 0.18, 1);
}
.spec {
  display: inline-block;
  font-size: 2rem;
  font-weight: 300;
  color: var(--color-text-secondary);
  opacity: 0;
  transform: translateX(2em);
}
.spec.active {
  opacity: 1;
  transform: translateX(0);
}

.hint {
  display: flex;
  position: fixed;
  align-items: center;
  gap: 0.5rem;
  bottom: 2rem;
  color: var(--color-text-secondary);

--hint-fade-y-offset: -1rem;
--hint-text-y-offset: -0.5rem;
  animation: hintFade infinite 3s cubic-bezier(0, 1, 0.18, 1);
}
.hint > .swipe-text {
  display: none;
}
.hint > span {
  animation: hintText infinite 3s;
}
.hint > svg {
  transform: scale(0.5);
}

@media (max-width: 800px) {
  .surname-start {
    padding-left: 0.5rem;
  }

  .hint {
    --hint-fade-y-offset: 1rem;
    --hint-text-y-offset: 0.5rem;
  }
  .hint > .swipe-text {
    display: initial;
  }
  .hint > .scroll-text {
    display: none;
  }
  .hint > svg {
    transform: scale(0.5) rotateZ(180deg);
  }
}

@keyframes hintFade {
  0%, 100% {
    opacity: 0;
    transform: translateY(var(--hint-fade-y-offset));
  }

  40% {
    opacity: 1;
  }

  80% {
    opacity: 0;
    transform: translateY(0rem);
  }
}

@keyframes hintText {
  0%, 100% {
    transform: translateY(var(--hint-text-y-offset));
  }

  80% {
    transform: translateY(0rem);
  }
}
</style>
