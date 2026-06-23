<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import excelLogo from '../assets/Microsoft_Office_Excel.png'
import bigQueryLogo from '../assets/BigQuery.png'
import pythonLogo from '../assets/Python.png'
import tableauLogo from '../assets/Tableau-Logo.png'
import powerBILogo from '../assets/Power-BI-Logo-2013.png'
import profileImg from '../assets/profile.jpeg'
import itkLogo from '../assets/itk-logo.png'
import revouLogo from '../assets/RevoU_Logo.png'
import featured1 from '../assets/featured1.jpg'
import featured2 from '../assets/featured2.jpg'

/* ═══════════════════════════════════════════════
   Dark Mode
   ═══════════════════════════════════════════════ */
const isDark = ref(false)

function applyTheme(dark) {
  isDark.value = dark
  if (dark) {
    document.documentElement.classList.add('dark')
  } else {
    document.documentElement.classList.remove('dark')
  }
}

function toggleDark() {
  const next = !isDark.value
  applyTheme(next)
  localStorage.setItem('theme', next ? 'dark' : 'light')
}

/* ═══════════════════════════════════════════════
   Scroll reveal via IntersectionObserver
   ═══════════════════════════════════════════════ */
let observer = null

function initObserver() {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.remove('opacity-0', 'translate-y-8')
          entry.target.classList.add('opacity-100', 'translate-y-0')
          observer.unobserve(entry.target)
        }
      })
    },
    { threshold: 0.1 }
  )
  document.querySelectorAll('.reveal').forEach((el) => observer.observe(el))
}

/* ═══════════════════════════════════════════════
   Mobile nav
   ═══════════════════════════════════════════════ */
const mobileOpen = ref(false)

/* ═══════════════════════════════════════════════
   Navbar scroll shadow
   ═══════════════════════════════════════════════ */
const scrolled = ref(false)
function onScroll() {
  scrolled.value = window.scrollY > 10
}

/* ═══════════════════════════════════════════════
   Lifecycle
   ═══════════════════════════════════════════════ */
onMounted(() => {
  // Theme init
  const saved = localStorage.getItem('theme')
  if (saved === 'dark' || (!saved && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
    applyTheme(true)
  } else {
    applyTheme(false)
  }

  // Scroll observer
  initObserver()

  // Navbar shadow
  window.addEventListener('scroll', onScroll, { passive: true })
})

onBeforeUnmount(() => {
  if (observer) observer.disconnect()
  window.removeEventListener('scroll', onScroll)
})

/* ═══════════════════════════════════════════════
   Static Data
   ═══════════════════════════════════════════════ */
const navLinks = [
 { label: 'Home', href: '#home' },
 { label: 'About', href: '#about' },
 { label: 'Education', href: '#education' },
 { label: 'Experience', href: '#experience' },
 { label: 'Projects', href: '#projects' },
 { label: 'Skills', href: '#skills' },
 { label: 'Contact', href: '#contact' },
]

const skills = [
  { name: 'Excel',        logo: excelLogo },
  { name: 'BigQuery SQL', logo: bigQueryLogo },
  { name: 'Python',       logo: pythonLogo },
  { name: 'Tableau',      logo: tableauLogo },
  { name: 'Power BI',     logo: powerBILogo },
]

const softSkills = [
  { name: 'Problem Solving', icon: '🧠', gradient: 'from-emerald-400 to-teal-600 dark:from-emerald-500 dark:to-teal-700' },
  { name: 'Communication', icon: '💬', gradient: 'from-sky-400 to-blue-600 dark:from-sky-500 dark:to-blue-700' },
  { name: 'Critical Thinking', icon: '🤔', gradient: 'from-yellow-400 to-amber-600 dark:from-yellow-500 dark:to-amber-700' },
  { name: 'Team Collaboration', icon: '🤝', gradient: 'from-indigo-400 to-violet-600 dark:from-indigo-500 dark:to-violet-700' },
  { name: 'Adaptability', icon: '🌟', gradient: 'from-orange-400 to-red-500 dark:from-orange-500 dark:to-red-600' },
]

const experiences = [
  {
    period: 'Nov 2025 - May 2026',
    role: 'Archivist Intern',
    company: 'Rumah Detensi Imigrasi Balikpapan',
    desc: '● Organized yearly archives for Rudenim Balikpapan from 2005–2020, transferring more than 2,000 records into Microsoft Excel to support timely cataloging and document destruction after retention expiry.\n● Created an Excel dashboard to centralize detainee health checkup records and monthly reports, reducing administrative processing time by 40%.',
  },
  {
    period: 'Dec 2023 - Feb 2024',
    role: 'Administration Intern',
    company: 'PT. Bahana Cipta Internusa',
    desc: '● Created an elevation-based drainage routing model and drainage channel layout to support early-stage drainage planning for the RDMP project.\n● Managed daily data extraction, validation, and entry from 5 high-volume Excel spreadsheets into the company\'s database, maintaining 100% data accuracy and eliminating processing backlogs for 25+ files weekly.',
  },
]

const educations = [
  {
    logo: itkLogo,
    school: 'Institut Teknologi Kalimantan',
    period: 'Jul 2021 - Apr 2025',
    degree: 'Bachelor, Mathematics',
    gpa: 'GPA: 3.60 / 4.00',
    description:
      'Specialized in Statistics and Applied Mathematics. Completed a thesis in Graph Theory and Max-Plus Algebra focusing on optimizing traffic light timing to reduce street congestion.',
  },

  {
    logo: revouLogo,
    school: 'RevoU',
    period: 'Feb 2026 - Present',
    degree: 'Full Stack Data Analysis Course',
    gpa: '',
    description:
      'Covered the complete data analytics lifecycle, from defining business problems and hypotheses to data collection, cleaning, analysis, visualization, and presenting actionable insights using SQL, Python, Tableau, and Power BI.',
  },
]

const featuredProjects = [
  {
    title: 'Enhancing Credit Card Profitability Through Risk and Behavioral Segmentation',
    image: featured1,
    tech: ['Python', 'K-Means', 'EDA'],

    background:
      'RevoBank aimed to increase credit card profitability by encouraging greater credit card usage among existing customers. Rising fraud losses threatened revenue, requiring a data-driven approach to balance business growth with risk management.',

    methods: [
      'Data cleaning and preprocessing using Python',
      'Feature engineering for customer risk metrics',
      'Customer segmentation using K-Means clustering',
      'Exploratory Data Analysis (EDA)',
    ],

    findings:
      'Fraud accounted for 14.8% of gross revenue (IDR 1.01B), while non-retired customers exhibited the highest fraud risk and transaction volatility.',

    actions:
      'Increase credit limits for low-risk mid-career customers and introduce lifestyle reward programs for the Stable Silver Giants customer segment.',

    slides:
      'https://drive.google.com/file/d/1Q-d3Jci1eCg1TQn0Usxo7FbUoWTPu6Zt/view?usp=sharing',

    code:
      'https://colab.research.google.com/drive/17D6kwVJDcd5rVtSJ76BI0LviOinYjyCM?usp=sharing',
  },

  {
    title: 'Brazil Good Deals Market (BGDMart) Regional Revenue & Logistics Optimization',
    image: featured2,
    tech: ['SQL', 'Python', 'Tableau'],

    background:
      'BGDMart experienced growing regional demand across Brazil. Improving logistics efficiency and delivery performance became essential to sustain customer satisfaction and revenue growth.',

    methods: [
      'SQL for data cleaning and joins',
      'Python for Exploratory Data Analysis',
      'Customer clustering',
      'Tableau dashboard development',
    ],

    findings:
      'The top five Brazilian states generated 88% of total revenue, while Rio de Janeiro and Bahia recorded late delivery rates above 11%.',

    actions:
      'Establish regional fulfillment hubs in high-value states while prioritizing marketing investment toward regions with strong logistics performance.',

    slides:
      'https://drive.google.com/file/d/1xJgOhblrs2XTjaaPaPwF1HO77q8AtXCz/view?usp=drive_link',

    dashboard:
      'https://public.tableau.com/views/DATVIZDeepp/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link',

    code:
      'https://colab.research.google.com/drive/1Td_oA1G5W2bzYuimpSeKn9DpA-JUW-la?usp=sharing',
  },
]

const contactForm = ref({ name: '', email: '', message: '' })

function handleSubmit() {
  alert(`Thank you, ${contactForm.value.name}! Your message has been sent.`)
  contactForm.value = { name: '', email: '', message: '' }
}
</script>

<template>
  <!-- Root wrapper — handles light/dark background & text -->
  <div
    class="min-h-screen font-sans antialiased transition-colors duration-300"
    :class="isDark
      ? 'bg-[#0f1117] text-stone-300'
      : 'bg-stone-50 text-stone-700'"
  >

    <!-- ════════════════════════════════════════════
         NAVBAR
         ════════════════════════════════════════════ -->
    <nav
      class="fixed top-0 inset-x-0 z-50 transition-all duration-300 border-b"
      :class="[
        isDark
          ? 'bg-[#0f1117]/80 border-stone-800/60'
          : 'bg-white/80 border-stone-200/60',
        scrolled ? 'shadow-lg backdrop-blur-xl' : 'backdrop-blur-md'
      ]"
    >
      <div class="max-w-6xl mx-auto flex items-center justify-between px-6 h-16">
        <!-- Logo -->
        <a href="#" class="flex items-center gap-2.5 group">
          <span class="inline-flex items-center justify-center w-9 h-9 rounded-xl bg-gradient-to-br from-rose-400 to-rose-600 text-white text-sm font-black shadow-lg shadow-rose-500/25 group-hover:shadow-rose-500/40 transition-shadow duration-300">R</span>
          <span class="text-xl font-bold tracking-tight" :class="isDark ? 'text-white' : 'text-stone-900'">Rafli</span>
        </a>

        <!-- Desktop links -->
        <div class="hidden md:flex items-center gap-1">
          <a
            v-for="link in navLinks"
            :key="link.href"
            :href="link.href"
            class="px-3.5 py-2 rounded-lg text-sm font-medium transition-all duration-200"
            :class="isDark
              ? 'text-stone-400 hover:text-rose-400 hover:bg-rose-500/10'
              : 'text-stone-600 hover:text-rose-600 hover:bg-rose-50'"
          >{{ link.label }}</a>
        </div>

        <!-- Right actions -->
        <div class="flex items-center gap-3">
          <!-- Dark / Light toggle -->
          <button
            id="dark-toggle"
            @click="toggleDark"
            class="relative w-[52px] h-7 rounded-full transition-colors duration-300 focus:outline-none focus:ring-2 focus:ring-rose-400 focus:ring-offset-2 cursor-pointer"
            :class="isDark
              ? 'bg-stone-700 focus:ring-offset-[#0f1117]'
              : 'bg-stone-200 focus:ring-offset-white'"
            :aria-label="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
          >
            <span
              class="absolute top-0.5 left-0.5 w-6 h-6 rounded-full shadow-md flex items-center justify-center text-xs transition-all duration-300"
              :class="isDark
                ? 'translate-x-[24px] bg-stone-900'
                : 'translate-x-0 bg-white'"
            >{{ isDark ? '🌙' : '☀️' }}</span>
          </button>

          <!-- Hamburger (mobile) -->
          <button
            id="mobile-menu-toggle"
            @click="mobileOpen = !mobileOpen"
            class="md:hidden p-2 rounded-lg transition-colors cursor-pointer"
            :class="isDark ? 'hover:bg-stone-800' : 'hover:bg-stone-100'"
            aria-label="Toggle menu"
          >
            <svg class="w-5 h-5" :class="isDark ? 'text-stone-300' : 'text-stone-700'" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
              <path v-if="!mobileOpen" stroke-linecap="round" d="M4 6h16M4 12h16M4 18h16" />
              <path v-else stroke-linecap="round" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
      </div>

      <!-- Mobile dropdown -->
      <transition
        enter-active-class="transition duration-200 ease-out"
        enter-from-class="opacity-0 -translate-y-2"
        enter-to-class="opacity-100 translate-y-0"
        leave-active-class="transition duration-150 ease-in"
        leave-from-class="opacity-100 translate-y-0"
        leave-to-class="opacity-0 -translate-y-2"
      >
        <div
          v-if="mobileOpen"
          class="md:hidden border-t backdrop-blur-xl"
          :class="isDark
            ? 'bg-[#0f1117]/95 border-stone-800'
            : 'bg-white/95 border-stone-200'"
        >
          <div class="px-4 py-3 flex flex-col gap-1">
            <a
              v-for="link in navLinks"
              :key="link.href"
              :href="link.href"
              @click="mobileOpen = false"
              class="px-4 py-2.5 rounded-lg text-sm font-medium transition-all"
              :class="isDark
                ? 'text-stone-400 hover:text-rose-400 hover:bg-rose-500/10'
                : 'text-stone-600 hover:text-rose-600 hover:bg-rose-50'"
            >{{ link.label }}</a>
          </div>
        </div>
      </transition>
    </nav>

    <!-- ════════════════════════════════════════════
         HERO — photo left, text right
         ════════════════════════════════════════════ -->
    <section id="home" class="pt-28 sm:pt-36 pb-20 px-6">
      <div class="max-w-5xl mx-auto flex flex-col md:flex-row items-center gap-12 md:gap-16">

        <!-- Left: Photo / Avatar -->
        <div class="flex-shrink-0 reveal opacity-0 translate-y-8 transition-all duration-700">
          <div class="relative">
            <!-- Glow ring -->
            <div class="absolute -inset-3 rounded-full bg-gradient-to-br from-rose-400/30 to-rose-600/20 blur-xl animate-pulse"></div>
            <!-- Photo container -->
            <div class="relative w-48 h-48 sm:w-56 sm:h-56 rounded-full bg-gradient-to-br from-rose-300 to-rose-500 p-1 shadow-2xl shadow-rose-500/20">
              <img
                :src="profileImg"
                alt="Profile Photo"
                class="w-full h-full rounded-full object-cover"
              />
            </div>
            <!-- Floating accent dot -->
            <div class="absolute -bottom-2 -right-2 w-8 h-8 rounded-full bg-gradient-to-br from-rose-400 to-rose-600 shadow-lg shadow-rose-500/30 flex items-center justify-center text-white text-xs font-bold">✓</div>
          </div>
        </div>

        <!-- Right: Text content -->
        <div class="flex-1 text-center md:text-left">
          <!-- Badge -->
          <div class="reveal opacity-0 translate-y-8 transition-all duration-700 delay-100 mb-5">
            <span
              class="inline-flex items-center gap-2 px-4 py-1.5 rounded-full text-xs font-semibold tracking-wide uppercase border"
              :class="isDark
                ? 'bg-rose-950/40 text-rose-400 border-rose-800/40'
                : 'bg-rose-100 text-rose-700 border-rose-200/60'"
            >
              <span class="relative flex h-2 w-2">
                <span class="absolute inline-flex h-full w-full rounded-full bg-rose-400 opacity-75 animate-ping"></span>
                <span class="relative inline-flex h-2 w-2 rounded-full bg-rose-500"></span>
              </span>
              Open to Opportunities
            </span>
          </div>

          <h1
            class="reveal opacity-0 translate-y-8 transition-all duration-700 delay-150 text-4xl sm:text-5xl font-extrabold tracking-tight leading-tight text-stone-900 dark:text-white"
          >
            Hi! I'm
            <span class="text-3xl sm:text-4xl lg:text-5xl bg-gradient-to-r from-rose-500 to-rose-600 bg-clip-text text-transparent">
              Rafli El'riza Budiman
            </span>
          </h1>

          <p
            class="reveal opacity-0 translate-y-8 transition-all duration-700 delay-200 mt-5 text-lg sm:text-xl leading-relaxed max-w-xl text-stone-500 dark:text-stone-400"
          >A passionate Data Analyst who loves transforming complex data into clear, actionable insights to drive informed decisions.
          </p>

          <!-- CTA -->
          <div class="reveal opacity-0 translate-y-8 transition-all duration-700 delay-300 mt-8 flex flex-wrap items-center gap-4 justify-center md:justify-start">
            <a
              href="#projects"
              class="inline-flex items-center gap-2 px-6 py-3 rounded-xl bg-gradient-to-r from-rose-500 to-rose-600 hover:from-rose-600 hover:to-rose-700 text-white font-semibold text-sm shadow-lg shadow-rose-500/25 hover:shadow-xl hover:shadow-rose-500/35 transition-all duration-300 hover:-translate-y-0.5"
            >
              View Projects
              <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M19 9l-7 7-7-7"/></svg>
            </a>
            <a
              href="#contact"
              class="inline-flex items-center gap-2 px-6 py-3 rounded-xl border font-semibold text-sm transition-all duration-300 hover:-translate-y-0.5"
              :class="isDark
                ? 'border-stone-700 text-stone-300 hover:border-rose-500 hover:text-rose-400'
                : 'border-stone-300 text-stone-700 hover:border-rose-400 hover:text-rose-600'"
            >Contact Me</a>
          </div>
        </div>
      </div>
    </section>

    <!-- ════════════════════════════════════════════
         ABOUT ME
         ════════════════════════════════════════════ -->
    <section id="about" class="py-20 px-6 transition-colors duration-300" :class="isDark ? 'bg-[#13151d]' : 'bg-white/60'">
      <div class="max-w-4xl mx-auto">
        <div class="text-center reveal opacity-0 translate-y-8 transition-all duration-700">
          <span
            class="inline-block px-3 py-1 rounded-full text-xs font-semibold tracking-wide uppercase mb-4"
            :class="isDark ? 'bg-rose-950/40 text-rose-400' : 'bg-rose-100 text-rose-600'"
          >Introduction</span>
          <h2 class="text-3xl sm:text-4xl font-bold" :class="isDark ? 'text-white' : 'text-stone-900'">About Me</h2>
        </div>
        
        <div class="mt-10 reveal opacity-0 translate-y-8 transition-all duration-700 text-base sm:text-lg leading-relaxed text-justify" :class="isDark ? 'text-stone-400' : 'text-stone-600'">
          <p class="mb-4">
            I am an aspiring Data Analyst with a strong mathematics background and an interest in using data to support decision-making. Through my experience as a Archivist and analytics projects, I have used SQL, Python, Microsoft Excel, Tableau, and Power BI to analyze data, build dashboards, and present findings. I organized and cataloged more than 2,000 archives and developed an Excel dashboard that reduced administrative process time by 40%.
          </p>
          <p>
            These experiences strengthened my Statistical Skills, EDA, and Business Intelligence while improving communication, teamwork, leadership, adaptability, and problem-solving skills also working with diverse stakeholders. I am eager to apply my analytical skills to solve business problems and continue growing as a Data Analyst.
          </p>
        </div>
      </div>
    </section>


    <!-- ════════════════════════════════════════════
     EDUCATION
    ════════════════════════════════════════════ -->
    <section
      id="education"
      class="py-20 px-6 transition-colors duration-300"
      :class="isDark ? 'bg-[#13151d]' : 'bg-white/60'"
    >
      <div class="max-w-6xl mx-auto">

        <!-- Heading -->
        <div class="text-center reveal opacity-0 translate-y-8 transition-all duration-700">
          <span
            class="inline-block px-3 py-1 rounded-full text-xs font-semibold tracking-wide uppercase mb-4"
            :class="isDark
              ? 'bg-rose-950/40 text-rose-400'
              : 'bg-rose-100 text-rose-600'"
          >
            Education
          </span>

          <h2
            class="text-3xl sm:text-4xl font-bold"
            :class="isDark ? 'text-white' : 'text-stone-900'"
          >
            Education
          </h2>

          <p
            class="mt-3"
            :class="isDark ? 'text-stone-400' : 'text-stone-500'"
          >
            Academic background and certifications.
          </p>
        </div>

        <!-- Cards -->
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mt-14">

          <div
            v-for="(edu,i) in educations"
            :key="edu.school"
            class="reveal opacity-0 translate-y-8 transition-all duration-700 rounded-3xl border p-8 shadow-lg hover:-translate-y-1 hover:shadow-2xl"
            :style="{ transitionDelay: `${(i+1)*150}ms` }"
            :class="isDark
              ? 'bg-[#181a24] border-stone-800 hover:border-rose-700'
              : 'bg-white border-stone-200 hover:border-rose-300'"
          >

            <!-- Logo -->
            <div class="flex justify-center">
              <div class="w-24 h-24 rounded-full bg-white shadow-lg flex items-center justify-center">
                <img
                  :src="edu.logo"
                  :alt="edu.school"
                  class="w-16 h-16 object-contain"
                >
              </div>
            </div>

            <!-- School -->
            <div class="text-center mt-6">

              <h3
                class="text-2xl font-bold"
                :class="isDark ? 'text-white' : 'text-stone-900'"
              >
                {{ edu.school }}
              </h3>

              <span
                class="inline-block mt-3 px-4 py-1 rounded-full text-xs font-semibold"
                :class="isDark
                  ? 'bg-rose-900/30 text-rose-300'
                  : 'bg-rose-100 text-rose-600'"
              >
                {{ edu.period }}
              </span>

            </div>

            <!-- Degree -->
            <div class="mt-7 text-center">

              <h4
                class="text-lg font-bold"
                :class="isDark ? 'text-rose-300' : 'text-rose-600'"
              >
                {{ edu.degree }}
              </h4>

              <p
                v-if="edu.gpa"
                class="mt-2 text-sm font-semibold"
                :class="isDark ? 'text-stone-300' : 'text-stone-600'"
              >
                {{ edu.gpa }}
              </p>

            </div>

            <!-- Description -->
            <p
              class="mt-6 text-sm leading-7 text-center"
              :class="isDark ? 'text-stone-400' : 'text-stone-600'"
            >
              {{ edu.description }}
            </p>

          </div>

        </div>

      </div>
    </section>

    <!-- ════════════════════════════════════════════
         EXPERIENCE
         ════════════════════════════════════════════ -->
    <section id="experience" class="py-20 px-6">
      <div class="max-w-3xl mx-auto">
        <div class="text-center reveal opacity-0 translate-y-8 transition-all duration-700">
          <span
            class="inline-block px-3 py-1 rounded-full text-xs font-semibold tracking-wide uppercase mb-4"
            :class="isDark ? 'bg-rose-950/40 text-rose-400' : 'bg-rose-100 text-rose-600'"
          >Experience</span>
          <h2 class="text-3xl sm:text-4xl font-bold" :class="isDark ? 'text-white' : 'text-stone-900'">Career History</h2>
        </div>

        <!-- Timeline -->
        <div class="mt-14 relative">
          <!-- Vertical line -->
          <div
            class="absolute left-4 sm:left-6 top-0 bottom-0 w-px bg-gradient-to-b from-rose-400 via-rose-300 to-transparent"
            :class="isDark ? 'opacity-50' : 'opacity-70'"
          ></div>

          <div
            v-for="(exp, i) in experiences"
            :key="i"
            class="reveal opacity-0 translate-y-8 transition-all duration-700 relative pl-12 sm:pl-16 pb-12 last:pb-0"
            :style="{ transitionDelay: `${(i + 1) * 150}ms` }"
          >
            <!-- Dot -->
            <div
              class="absolute left-2.5 sm:left-4 top-1.5 w-3.5 h-3.5 rounded-full bg-rose-400 ring-4"
              :class="isDark ? 'ring-[#0f1117]' : 'ring-stone-50'"
            ></div>

            <div
              class="p-5 sm:p-6 rounded-2xl border shadow-sm hover:shadow-md transition-all duration-300"
              :class="isDark
                ? 'bg-[#181a24] border-stone-800/80 hover:border-rose-800/50'
                : 'bg-white border-stone-200/80 hover:border-rose-200'"
            >
              <span class="text-xs font-semibold text-rose-500 tracking-wide uppercase">{{ exp.period }}</span>
              <h3 class="mt-1.5 text-lg font-bold" :class="isDark ? 'text-white' : 'text-stone-900'">{{ exp.role }}</h3>
              <p class="text-sm font-medium" :class="isDark ? 'text-stone-400' : 'text-stone-500'">{{ exp.company }}</p>
              <p class="mt-2 text-sm leading-relaxed whitespace-pre-line" :class="isDark ? 'text-stone-400' : 'text-stone-600'">{{ exp.desc }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ════════════════════════════════════════════
         PROJECTS
         ════════════════════════════════════════════ -->
    <section
      id="projects"
      class="py-20 px-6 transition-colors duration-300"
      :class="isDark ? 'bg-[#13151d]' : 'bg-white/60'"
    >
      <div class="max-w-7xl mx-auto">

        <!-- Heading -->
        <div class="text-center reveal opacity-0 translate-y-8 transition-all duration-700">
          <span
            class="inline-block px-3 py-1 rounded-full text-xs font-semibold tracking-wide uppercase mb-4"
            :class="isDark ? 'bg-rose-950/40 text-rose-400' : 'bg-rose-100 text-rose-600'"
          >
            Portfolio
          </span>

          <h2
            class="text-3xl sm:text-4xl font-bold"
            :class="isDark ? 'text-white' : 'text-stone-900'"
          >
            Featured Projects
          </h2>

          <p
            class="mt-3"
            :class="isDark ? 'text-stone-400' : 'text-stone-500'"
          >
            My most advanced analytics projects.
          </p>
        </div>

        <!-- Featured -->
        <div class="grid lg:grid-cols-2 gap-8 mt-14">

          <div
            v-for="(project, i) in featuredProjects"
            :key="project.title"
            class="reveal opacity-0 translate-y-8 transition-all duration-700 rounded-3xl overflow-hidden border shadow-lg"
            :style="{ transitionDelay: `${(i+1)*150}ms` }"
            :class="isDark
              ? 'bg-[#181a24] border-stone-800 hover:border-rose-700'
              : 'bg-white border-stone-200 hover:border-rose-300'"
          >

            <!-- Image -->
            <img
              :src="project.image"
              :alt="project.title"
              class="w-full h-60 object-cover object-top"
            >

            <div class="p-7">

              <h3
                class="text-xl font-bold"
                :class="isDark ? 'text-white' : 'text-stone-900'"
              >
                {{ project.title }}
              </h3>

              <!-- Tech -->
              <div class="flex flex-wrap gap-2 mt-4 mb-6">
                <span
                  v-for="tool in project.tech"
                  :key="tool"
                  class="px-3 py-1 rounded-full text-xs font-semibold"
                  :class="isDark
                    ? 'bg-rose-900/30 text-rose-300'
                    : 'bg-rose-100 text-rose-600'"
                >
                  {{ tool }}
                </span>
              </div>

              <div class="space-y-5 text-sm">

                <div>
                  <h4 class="font-bold mb-1">Background</h4>
                  <p>{{ project.background }}</p>
                </div>

                <div>
                  <h4 class="font-bold mb-1">Methods</h4>

                  <ul class="list-disc ml-5 space-y-1">
                    <li
                      v-for="method in project.methods"
                      :key="method"
                    >
                      {{ method }}
                    </li>
                  </ul>
                </div>

                <div>
                  <h4 class="font-bold mb-1">Key Findings</h4>
                  <p>{{ project.findings }}</p>
                </div>

                <div>
                  <h4 class="font-bold mb-1">Business Actions</h4>
                  <p>{{ project.actions }}</p>
                </div>

              </div>

              <!-- Buttons -->
              <div class="grid grid-cols-2 gap-3 mt-8">

                <a
                  :href="project.slides"
                  target="_blank"
                  class="text-center py-3 rounded-xl bg-rose-500 text-white font-semibold hover:bg-rose-600 transition"
                >
                  Open Slides
                </a>

                <a
                  :href="project.code"
                  target="_blank"
                  class="text-center py-3 rounded-xl border font-semibold transition"
                  :class="isDark
                    ? 'border-stone-700 hover:bg-stone-800'
                    : 'border-stone-300 hover:bg-stone-100'"
                >
                  Open Code
                </a>

                <a
                  v-if="project.dashboard"
                  :href="project.dashboard"
                  target="_blank"
                  class="col-span-2 text-center py-3 rounded-xl border font-semibold transition"
                  :class="isDark
                    ? 'border-stone-700 hover:bg-stone-800'
                    : 'border-stone-300 hover:bg-stone-100'"
                >
                  Open Dashboard
                </a>

              </div>

            </div>

          </div>

        </div>

        <!-- Intermediate -->
        <div class="mt-24 text-center">
          <h2 class="text-3xl font-bold">Intermediate Projects</h2>
          <p class="mt-3 text-stone-500">Coming Soon</p>
        </div>

        <!-- Foundational -->
        <div class="mt-16 text-center">
          <h2 class="text-3xl font-bold">Foundational Projects</h2>
          <p class="mt-3 text-stone-500">Coming Soon</p>
        </div>

      </div>
    </section>

    <!-- ════════════════════════════════════════════
         SKILLS
         ════════════════════════════════════════════ -->
    <section
      id="skills"
      class="py-20 px-6 transition-colors duration-300"
    >
      <div class="max-w-4xl mx-auto text-center">
        <div class="reveal opacity-0 translate-y-8 transition-all duration-700">
          <span
            class="inline-block px-3 py-1 rounded-full text-xs font-semibold tracking-wide uppercase mb-4"
            :class="isDark ? 'bg-rose-950/40 text-rose-400' : 'bg-rose-100 text-rose-600'"
          >Skills</span>
          <h2 class="text-3xl sm:text-4xl font-bold" :class="isDark ? 'text-white' : 'text-stone-900'">Tech Stack</h2>
          <p class="mt-3" :class="isDark ? 'text-stone-400' : 'text-stone-500'">Tools and technologies I am proficient in</p>
        </div>

        <div class="mt-14 flex flex-wrap justify-center gap-8 sm:gap-12">
          <div
            v-for="(skill, i) in skills"
            :key="skill.name"
            class="reveal opacity-0 translate-y-8 transition-all duration-700 group flex flex-col items-center gap-3"
            :style="{ transitionDelay: `${(i + 1) * 100}ms` }"
          >
            <div
              class="w-20 h-20 sm:w-24 sm:h-24 rounded-full bg-white dark:bg-[#181a24] border border-stone-200 dark:border-stone-800 shadow-lg flex items-center justify-center group-hover:scale-110 group-hover:shadow-xl transition-all duration-300 cursor-default group-hover:border-rose-400 dark:group-hover:border-rose-500"
            >
              <img :src="skill.logo" :alt="skill.name" class="w-10 h-10 sm:w-12 sm:h-12 object-contain drop-shadow-sm" />
            </div>
            <span class="text-sm font-semibold" :class="isDark ? 'text-stone-300' : 'text-stone-700'">{{ skill.name }}</span>
          </div>
        </div>

        <!-- Soft Skills -->
        <div class="mt-20 reveal opacity-0 translate-y-8 transition-all duration-700">
          <h2 class="text-2xl sm:text-3xl font-bold" :class="isDark ? 'text-white' : 'text-stone-900'">Soft Skills</h2>
          <p class="mt-3" :class="isDark ? 'text-stone-400' : 'text-stone-500'">My interpersonal skills</p>
        </div>

        <div class="mt-10 flex flex-wrap justify-center gap-3 sm:gap-4">
          <div
            v-for="(skill, i) in softSkills"
            :key="skill.name"
            class="reveal opacity-0 translate-y-8 transition-all duration-700 flex items-center gap-2 px-4 py-2 sm:px-5 sm:py-2.5 rounded-full border shadow-sm hover:shadow-md hover:-translate-y-0.5 transition-all duration-300 cursor-default bg-white border-stone-200 hover:border-rose-300 dark:bg-[#181a24] dark:border-stone-800 dark:hover:border-rose-700"
            :style="{ transitionDelay: `${(i + 1) * 100}ms` }"
          >
            <span class="text-lg sm:text-xl">{{ skill.icon }}</span>
            <span class="text-sm sm:text-base font-medium text-stone-700 dark:text-stone-300">{{ skill.name }}</span>
          </div>
        </div>
      </div>
    </section>

    <!-- ════════════════════════════════════════════
         CONTACT
         ════════════════════════════════════════════ -->
    <section id="contact" class="py-20 px-6 transition-colors duration-300" :class="isDark ? 'bg-[#13151d]' : 'bg-white/60'">
      <div class="max-w-2xl mx-auto">
        <div class="text-center reveal opacity-0 translate-y-8 transition-all duration-700">
          <span
            class="inline-block px-3 py-1 rounded-full text-xs font-semibold tracking-wide uppercase mb-4"
            :class="isDark ? 'bg-rose-950/40 text-rose-400' : 'bg-rose-100 text-rose-600'"
          >Contact</span>
          <h2 class="text-3xl sm:text-4xl font-bold" :class="isDark ? 'text-white' : 'text-stone-900'">Let's Connect</h2>
          <p class="mt-3" :class="isDark ? 'text-stone-400' : 'text-stone-500'">Have a question or want to collaborate? Feel free to reach out!</p>
        </div>

        <!-- Social links -->
        <div class="reveal opacity-0 translate-y-8 transition-all duration-700 mt-10 flex justify-center gap-4 flex-wrap">
          <a
            v-for="social in [
              { href: 'https://www.linkedin.com/in/rafli-elriza-budiman', label: 'LinkedIn', icon: 'linkedin' },
              { href: 'https://github.com/raflielrizabudiman', label: 'GitHub', icon: 'github' },
              { href: 'mailto:raflielrizabudiman@gmail.com', label: 'Email', icon: 'email' },
            ]"
            :key="social.label"
            :href="social.href"
            target="_blank"
            class="inline-flex items-center gap-2 px-5 py-2.5 rounded-xl border text-sm font-medium shadow-sm hover:shadow-md transition-all duration-300"
            :class="isDark
              ? 'bg-[#181a24] border-stone-800 text-stone-300 hover:border-rose-700 hover:text-rose-400'
              : 'bg-white border-stone-200 text-stone-700 hover:border-rose-300 hover:text-rose-600'"
          >
            <!-- LinkedIn -->
            <svg v-if="social.icon === 'linkedin'" class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
            <!-- GitHub -->
            <svg v-if="social.icon === 'github'" class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg>
            <!-- Email -->
            <svg v-if="social.icon === 'email'" class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
            {{ social.label }}
          </a>
        </div>
      </div>
    </section>

    <!-- ════════════════════════════════════════════
         FOOTER
         ════════════════════════════════════════════ -->
    <footer
      class="py-8 px-6 border-t transition-colors duration-300"
      :class="isDark ? 'border-stone-800/60' : 'border-stone-200/60'"
    >
      <div class="max-w-6xl mx-auto flex flex-col sm:flex-row items-center justify-center gap-4 text-sm text-stone-500">
        <p>&copy; {{ new Date().getFullYear() }} Rafli. All rights reserved.</p>
      </div>
    </footer>

  </div>
</template>
