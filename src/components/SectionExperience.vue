<script setup lang="ts">
import PageExperienceItem from '@/components/SectionExperienceItem.vue'
import { computed } from 'vue'
import { vIntersectionObserver } from '@vueuse/components'
import { animateBackgroundIntersectionWorks } from '@/three/animations'
import { useIntersectionAnimation } from '@/composables/intersectAnimation'

const experiences = [
  {
    title: '完成高考',
    year: '2022',
    description: '进入合肥工业大学软件学院学习',
  },
  {
    title: '阅读了《光荣与梦想》',
    year: '2022',
    description: '非常有趣的一部书',
  },
  {
    title: '参加软院Web前端训练营',
    year: '2023',
    description: '学到很多前端开发的知识',
  },
  {
    title: '暑假旅居上海',
    year: '2023',
    description: '立志走遍世界~',
  },
  {
    title: '办张健身卡',
    year: '2023',
    description: '狠狠强身健体',
  },
  {
    title: '获得院奖学金',
    year: '2023',
    description: '运气不错，小赚一笔',
  },
]

const { animationProgress, animateIntersection: onIntersectionTitle } = useIntersectionAnimation()

const animationTranslateTitle = computed(() => `${5 - animationProgress.value * 5}rem`)

const animationIntersectWorksThreshold = computed(() => 1 / experiences.length)
function onIntersection (entries: IntersectionObserverEntry[]) {
  const [{ isIntersecting }] = entries
  if (isIntersecting) {
    animateBackgroundIntersectionWorks()
  }
}
</script>

<template>
  <section
    v-intersection-observer="[onIntersection, { threshold: animationIntersectWorksThreshold }]"
    class="section-experiences"
  >
    <h2
      v-intersection-observer="[onIntersectionTitle, { threshold: 1 }]"
      class="title"
    >
      Experience
    </h2>
    <div class="experiences-list">
      <PageExperienceItem
        v-for="(ex, index) in experiences"
        :key="index"
        :title="ex.title"
        :year="ex.year"
        :description="ex.description"
      />
    </div>
  </section>
</template>

<style scoped>
.section-experiences{
  align-items: center;
  flex-direction: row;
  justify-content: flex-start;
  gap: 10rem;
  margin: 10rem 0;
}
.section-experiences> .experiences-list {
  display: flex;
  flex-direction: column;
  gap: 10rem;
}
.section-experiences> .title {
  align-self: flex-end;
  flex-shrink: 0;
  position: sticky;
  left: 0;
  bottom: 50%;
  margin: 2rem 0;
  opacity: v-bind(animationProgress);
  transform: translateY(v-bind(animationTranslateTitle));
}

@media (max-width: 800px) {
  .section-experiences> .title {
    transform: translateY(calc(v-bind(animationTranslateTitle) * var(--animation-values-coef)));
  }
}

@media (max-width: 1200px) {
  .section-experiences{
    flex-wrap: wrap;
    gap: 0;
  }
  .section-experiences> .experiences-list {
    gap: 5rem;
  }
  .section-experiences> .title {
    position: static;
    margin-bottom: 0;
  }
}
</style>
