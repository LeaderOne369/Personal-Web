<script setup lang="ts">
import Background from '@/components/BackgroundScene.vue'
import SectionTitle from '@/components/SectionTitle.vue'
import SectionAbout from '@/components/SectionAbout.vue'
import SectionExperience from '@/components/SectionExperience.vue'
import SectionContacts from '@/components/SectionContacts.vue'
import Danmaku from 'danmaku-vue'
import Message from './components/MessageComponent.vue'
import { onMounted, ref } from 'vue'
import gsap from 'gsap'

const sections = [
  { id: 'title', text: 'Title' },
  { id: 'about', text: 'About' },
  { id: 'experience', text: 'Experience' },
  { id: 'contacts', text: 'Contacts' },
]

const scrollToSection = (id: string) => {
  const targetElement = document.getElementById(id)
  if (targetElement) {
    targetElement.scrollIntoView({ behavior: 'smooth' })
  }
}

const message = ref(JSON.parse(sessionStorage.getItem('message') || '[]') || [])
const danmus = ref<Array<string>>([...message.value])
const danmakuRef = ref<InstanceType<typeof Danmaku>>(null)
const show = ref<boolean>(false)
const extraStyle = ref<string>('font-weight: bolder;')

const openMessage = () => {
  show.value = !show.value
  danmakuRef.value.play()
}

onMounted(() => {
  gsap.fromTo('.sider', { x: '100%', opacity: 0 },
              { x: '-40', opacity: 1, duration: 2, ease: 'power2.inOut' })
  gsap.fromTo('.messageBtn', { x: '100%', opacity: 0 }, { x: '-50%', opacity: 1, duration: 2, ease: 'power2.inOut' })
})
</script>

<template>
  <main>
    <SectionTitle
      id="title"
      class="snap-center"
    />
    <SectionAbout
      id="about"
      class="snap-center"
    />
    <SectionExperience id="experience" />
    
    <SectionContacts
      id="contacts"
      class="snap-center"
    />
    <div class="sider">
      <ul class="sider-list">
        <li
          v-for="section in sections"
          :key="section.id"
          class="sider-item"
          @click="scrollToSection(section.id)"
        >
          {{ section.text }}
        </li>
      </ul>
    </div>
    <span
      class="messageBtn"
      @click="openMessage"
    >
      <p>留言</p>
    </span>
  </main>
  <Danmaku
    ref="danmakuRef"
    :autoplay="false"
    :debounce="10"
    :danmus="danmus"
    :extra-style="extraStyle"
    class="danmus"
  />
  <Message
    v-if="show"
    ref="messageRef"
    class="message animate__animated animate__slideInUp"
  />
  <Background />
</template>

<style scoped>
@layer layout {
  main > section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    transition: margin 0.6s cubic-bezier(0, 1, 0.18, 1),
      gap 0.6s cubic-bezier(0, 1, 0.18, 1);
  }
  main > section > * {
    transform-origin: 50% 50%;
  }
  
  .snap-center {
    scroll-snap-align: center;
  }

}
.sider-list {
  list-style: none;
  padding: 0;
}

.sider {
  position: fixed;
  top: 0;
  right: 0;
  cursor: pointer;
  padding: 5px;
}

.messageBtn {
  position: fixed;
  bottom: 0;
  right: 0;
  cursor: pointer;
  margin: 2rem;
  width: 4rem;
  height: 4rem;
  border-radius: 50%;
  background: #ffffff;
  display: flex;
  align-items: center;
  justify-content: center; 
}

.messageBtn:hover {
  transform: scale(1.2);
  transition: transform 0.3s ease;
  background: #000;
  color: #fff;
}

.messageBtn > p {
  font-size: 1rem;
  font-weight: bold;
  user-select: none;
}

.danmus {
  position: fixed;
  top: 0;
  width: 100%;
  height: 30%;
  z-index: -1;
  background: transparent;
}

.sider-item {
  display: block; /* Make li a block element */
  cursor: pointer;
  margin: 10px;
  padding: 5px;
  border: none;
  font-weight: bolder;
  border-radius: 5px;
}


.sider-item:hover {
  background: #ffdae1;
  transform: translateX(-15px);
  transition: transform 1 ease;
}

.message {
  position: fixed;
  bottom: 2rem;
  right: 10%;
}
</style>
