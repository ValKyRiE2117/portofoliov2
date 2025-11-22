<template>
  <section id="skills" class="py-20">
    <div class="container mx-auto px-6">
      <h2 class="text-4xl font-bold text-center mb-12 gradient-text">
        Keahlian & Teknologi
      </h2>
      <div class="grid grid-cols-2 md:grid-cols-4 gap-6 max-w-4xl mx-auto">
        <div
          v-for="skill in skills"
          :key="skill.name"
          class="glass-card rounded-xl p-6 text-center hover:scale-105 transition-transform"
        >
          <i
            v-if="skill.icon"
            :class="`${skill.icon} text-4xl ${skill.color} mb-3`"
          ></i>
          <img
            v-else
            :src="skill.image"
            :alt="`${skill.name} Logo`"
            class="w-10 h-10 mx-auto mb-3"
          />
          <h3 class="font-semibold mb-1">{{ skill.name }}</h3>
          <p class="text-gray-400 text-xs">{{ skill.category }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
const skills = [
  {
    name: "HTML",
    icon: "fab fa-html5",
    color: "text-orange-500",
    category: "Frontend",
  },
  {
    name: "CSS",
    icon: "fab fa-css3-alt",
    color: "text-blue-500",
    category: "Frontend",
  },
  {
    name: "JavaScript",
    icon: "fab fa-js",
    color: "text-yellow-400",
    category: "Frontend",
  },
  {
    name: "Vue.js",
    icon: "fab fa-vuejs",
    color: "text-green-500",
    category: "Frontend",
  },
  {
    name: "Nuxt",
    image: "https://nuxt.com/assets/design-kit/icon-green.svg",
    category: "Frontend",
  },
  {
    name: "PHP",
    icon: "fab fa-php",
    color: "text-purple-400",
    category: "Backend",
  },
  {
    name: "Laravel",
    icon: "fab fa-laravel",
    color: "text-red-500",
    category: "Backend",
  },
  {
    name: "CodeIgniter",
    image: "https://cdn.worldvectorlogo.com/logos/codeigniter.svg",
    category: "Backend",
  },
  {
    name: "NextJS",
    icon: "fab fa-react",
    color: "text-cyan-300",
    category: "Frontend",
  },
  {
    name: "Tailwind CSS",
    image:
      "https://tailwindcss.com/_next/static/media/tailwindcss-mark.d52e9897.svg",
    category: "Frontend",
  },
  {
    name: "Bootstrap",
    icon: "fab fa-bootstrap",
    color: "text-purple-600",
    category: "Frontend",
  },
  {
    name: "MySQL",
    icon: "fas fa-database",
    color: "text-blue-400",
    category: "Database",
  },
  {
    name: "GIT",
    icon: "fa fa-brands fa-git-alt",
    color: "text-orange-600",
    category: "DevOps",
  },
  {
    name: "Figma",
    icon: "fab fa-figma",
    color: "text-pink-500",
    category: "Design",
  },
  {
    name: "Web Hosting",
    icon: "fas fa-globe",
    color: "text-green-400",
    category: "DevOps",
  },
];
</script>
