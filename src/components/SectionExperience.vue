<script setup lang="ts">
import PageExperienceItem from "@/components/SectionExperienceItem.vue";
import { computed } from "vue";
import { vIntersectionObserver } from "@vueuse/components";
import { animateBackgroundIntersectionWorks } from "@/three/animations";
import { useIntersectionAnimation } from "@/composables/intersectAnimation";

const experiences = [
  {
    title: "高考及大学入学",
    year: "2022",
    description:
      "以优异成绩考入合肥工业大学软件工程学院，开启软件工程专业本科学习生涯",
  },
  {
    title: "阅读《光荣与梦想》",
    year: "2022",
    description:
      "深入研读美国历史著作《光荣与梦想》，拓宽人文视野，培养历史思维",
  },
  {
    title: "软件学院Web前端训练营",
    year: "2023",
    description:
      "参与学院组织的Web前端开发训练营，系统学习前端技术栈，包括HTML、CSS、JavaScript及Vue.js框架",
  },
  {
    title: "暑期社会实践",
    year: "2023",
    description:
      "利用暑期时间赴上海开展社会实践，体验一线城市生活，拓宽视野并坚定职业发展方向",
  },
  {
    title: "健身塑形计划",
    year: "2023",
    description: "坚持健身锻炼，注重身心健康发展，培养自律生活习惯",
  },
  {
    title: "获得校级奖学金",
    year: "2023",
    description: "凭借优异学习成绩获得校级奖学金，认可了在学业上的努力与成果",
  },
  {
    title: "Java实训项目 - OTC项目管理系统",
    year: "2024.06-07",
    description:
      "担任项目组长，在《Java实训》课程中带领团队开发OTC项目管理系统，负责项目架构设计、团队协调及核心功能实现",
  },
  {
    title: "软件工程实训项目 - 知识共享平台",
    year: "2025.01-02",
    description:
      "担任项目组长，在《软件工程实训》课程中带领团队开发知识共享平台，负责需求分析、系统设计及项目管理",
  },
  {
    title: "企业实训项目 - 智慧医院客服系统",
    year: "2025.06-07",
    description:
      "担任项目组长，在《企业实训》课程中带领团队开发智慧医院客服系统，深入了解企业级应用开发流程",
  },
  {
    title: "TOEFL考试通过",
    year: "2025.08",
    description:
      "TOEFL考试总分110分，展现出扎实的英语听说读写能力，为未来国际交流奠定基础",
  },
  {
    title: "GRE考试通过",
    year: "2025.09",
    description:
      "GRE考试总分331分，Quantitative部分满分，体现出优秀的数学逻辑思维和分析能力",
  },
  {
    title: "IAV GmbH 上海研发中心实习",
    year: "2025.10",
    description:
      "加入IAV GmbH上海研发中心担任软件开发工程师，参与IAV与大众集团联合开发的自动驾驶测试与数据分析平台（VENAS Engine）研发工作",
  },
];

const { animationProgress, animateIntersection: onIntersectionTitle } =
  useIntersectionAnimation();

const animationTranslateTitle = computed(
  () => `${5 - animationProgress.value * 5}rem`
);

const animationIntersectWorksThreshold = computed(() => 1 / experiences.length);
function onIntersection(entries: IntersectionObserverEntry[]) {
  const [{ isIntersecting }] = entries;
  if (isIntersecting) {
    animateBackgroundIntersectionWorks();
  }
}
</script>

<template>
  <section
    v-intersection-observer="[
      onIntersection,
      { threshold: animationIntersectWorksThreshold },
    ]"
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
.section-experiences {
  align-items: center;
  flex-direction: row;
  justify-content: flex-start;
  gap: 10rem;
  margin: 10rem 0;
}
.section-experiences > .experiences-list {
  display: flex;
  flex-direction: column;
  gap: 10rem;
}
.section-experiences > .title {
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
  .section-experiences > .title {
    transform: translateY(
      calc(v-bind(animationTranslateTitle) * var(--animation-values-coef))
    );
  }
}

@media (max-width: 1200px) {
  .section-experiences {
    flex-wrap: wrap;
    gap: 0;
  }
  .section-experiences > .experiences-list {
    gap: 5rem;
  }
  .section-experiences > .title {
    position: static;
    margin-bottom: 0;
  }
}
</style>
