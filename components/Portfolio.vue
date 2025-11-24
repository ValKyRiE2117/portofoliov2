<template>
  <section id="portfolio" class="py-20">
    <div class="container mx-auto px-6">
      <h2 class="text-4xl font-bold text-center mb-8 gradient-text pb-1">
        Portofolio Saya
      </h2>

      <!-- Filter Chips -->
      <div class="flex flex-wrap justify-center gap-3 mb-12">
        <button
          v-for="category in categories"
          :key="category"
          @click="selectedCategory = category"
          class="px-6 py-2 rounded-full text-sm font-semibold transition-all duration-300"
          :class="
            selectedCategory === category
              ? 'bg-cyan-500 text-white'
              : 'bg-gray-800 text-gray-300 hover:bg-gray-700'
          "
        >
          {{ category }}
        </button>
      </div>

      <!-- Projects Grid -->
      <div class="grid md:grid-cols-2 gap-6 max-w-5xl mx-auto mb-12">
        <div
          v-for="project in paginatedProjects"
          :key="project.title"
          class="glass-card rounded-xl overflow-hidden hover:scale-105 transition-transform"
        >
          <NuxtImg
            :src="project.image"
            :alt="project.title"
            class="w-full object-cover"
            :class="project.aspectVideo ? 'aspect-video' : ''"
          />
          <div class="p-4 md:p-6">
            <span class="text-cyan-400 text-xs font-semibold">
              {{ project.type }}
            </span>
            <h3 class="text-xl font-bold mt-2 mb-3">{{ project.title }}</h3>
            <p class="text-gray-400 text-sm mb-4">{{ project.description }}</p>
            <div class="flex flex-wrap gap-1.5 sm:gap-2 mb-4">
              <span
                v-for="tech in project.technologies"
                :key="tech"
                class="px-2 sm:px-3 py-1 bg-gray-800 rounded-full text-xs whitespace-nowrap hover:bg-gray-700 transition-colors"
              >
                {{ tech }}
              </span>
            </div>
            <a
              :href="project.link"
              target="_blank"
              class="text-cyan-400 text-sm hover:underline"
            >
              <i class="fas fa-arrow-right mr-2"></i>View Project
            </a>
          </div>
        </div>
      </div>

      <!-- Pagination -->
      <div v-if="totalPages > 1" class="flex justify-center items-center gap-2">
        <button
          @click="currentPage--"
          :disabled="currentPage === 1"
          class="px-4 py-2 rounded-lg bg-gray-800 text-white disabled:opacity-50 disabled:cursor-not-allowed hover:bg-gray-700 transition-colors"
        >
          <i class="fas fa-chevron-left"></i>
        </button>

        <button
          v-for="page in totalPages"
          :key="page"
          @click="currentPage = page"
          class="px-4 py-2 rounded-lg transition-all duration-300"
          :class="
            currentPage === page
              ? 'bg-cyan-500 text-white'
              : 'bg-gray-800 text-gray-300 hover:bg-gray-700'
          "
        >
          {{ page }}
        </button>

        <button
          @click="currentPage++"
          :disabled="currentPage === totalPages"
          class="px-4 py-2 rounded-lg bg-gray-800 text-white disabled:opacity-50 disabled:cursor-not-allowed hover:bg-gray-700 transition-colors"
        >
          <i class="fas fa-chevron-right"></i>
        </button>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

const projects = [
  {
    image: "/assets/project-1.png",
    type: "Landing Page",
    title: "Website Profil Program Studi",
    description:
      "Mengembang & mengembangkan website profil program studi dengan desain modern dan responsive.",
    technologies: ["Laravel", "JQuery", "Filament", "Tailwind CSS"],
    link: "https://dti.dinus.ac.id/",
    category: "Website",
  },
  {
    image: "/assets/project-2.png",
    type: "Full Stack",
    title: "Sistem Monitoring Mahasiswa",
    description:
      "Sistem monitoring berbasis Website untuk pemantauan akademik mahasiswa.",
    technologies: ["Laravel", "Livewire", "MySQL", "Tailwind CSS"],
    link: "https://dti.dinus.ac.id/sistem-monitoring-mahasiswa/",
    category: "Website",
  },
  {
    image: "/assets/project-3.png",
    type: "Full Stack",
    title: "Website Ticketing - Sky Access Network",
    description:
      "Mengembangkan website ticketing sederhana dan landing page klien freelance.",
    technologies: ["Laravel", "JQuery", "MySQL", "Tailwind CSS"],
    link: "https://skyaccessnetwork.com/",
    category: "Website",
  },
  {
    image: "/assets/project-4.png",
    type: "Landing Page",
    title: "Website Busana Nyaman Pakai",
    description:
      "Website Landing Page CV Busana Nyaman Pakai - Produsen Toga Wisuda & Jas Almamater",
    technologies: ["Laravel", "Filament", "Tailwind CSS"],
    link: "https://konveksibusananyamanpakai.com/",
    category: "Website",
  },
  {
    image: "/assets/project-5.png",
    type: "Full Stack",
    title: "Website Wedding App - Ongoing",
    description: "Wesbite Booking Pernikahan Sederahana Full Stack",
    technologies: ["Laravel", "NextJS", "Filament", "Tailwind CSS"],
    link: "https://github.com/ValKyRiE2117/WeddingWebsite",
    aspectVideo: true,
    category: "Website",
  },
  {
    image: "/assets/project-9.png",
    type: "Backend",
    title: "Inventori - Ongoing",
    description: "Wesbite Backend REST API dengan Laravel + Filament",
    technologies: ["Laravel", "REST API", "Filament"],
    link: "https://github.com/ValKyRiE2117/inventori-toko",
    aspectVideo: true,
    category: "Website",
  },
  {
    image: "/assets/Project-8.png",
    type: "Frontend",
    title: "TravelHub - Ongoing",
    description: "Wesbite Travel Frontend dengan Nuxt + Tailwind CSS",
    technologies: ["Nuxt", "Vue.JS", "Tailwind CSS"],
    link: "https://travelhub-project.vercel.app/",
    category: "Website",
  },
  {
    image: "/assets/project-6.jpeg",
    type: "E - Commerce",
    title: "Website - VeggiePack",
    description: "Website E - Commerce Sederhana VeggiePack",
    technologies: ["CodeIgniter", "JQuery", "MySQL", "Bootstrap"],
    link: "https://github.com/ValKyRiE2117/VeggiePack",
    aspectVideo: true,
    category: "Website",
  },
  {
    image: "/assets/project-7.jpeg",
    type: "UI/UX",
    title: "Staybook App - Hotel Booking App",
    description: "Design UI/UX Aplikasi Booking Hotel Modern menggunakan Figma",
    technologies: ["Figma"],
    link: "https://www.figma.com/design/G3UGVmjjAkg2prKaucSWwQ/StayBook?node-id=0-1&t=lie0lWsCjvS8XXlC-1",
    category: "UI/UX",
  },
];

const categories = ["All", "Website", "Mobile", "UI/UX"];
const selectedCategory = ref("All");
const currentPage = ref(1);
const projectsPerPage = 4;

// Filter projects based on selected category
const filteredProjects = computed(() => {
  if (selectedCategory.value === "All") {
    return projects;
  }
  return projects.filter(
    (project) => project.category === selectedCategory.value
  );
});

// Calculate total pages
const totalPages = computed(() => {
  return Math.ceil(filteredProjects.value.length / projectsPerPage);
});

// Get projects for current page
const paginatedProjects = computed(() => {
  const start = (currentPage.value - 1) * projectsPerPage;
  const end = start + projectsPerPage;
  return filteredProjects.value.slice(start, end);
});

// Reset to page 1 when category changes
watch(selectedCategory, () => {
  currentPage.value = 1;
});
</script>
