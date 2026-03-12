<template>
  <div
    ref="appWrapper"
    class="app-wrapper grid-pattern font-primary h-full"
    id="appWrapper"
    :style="{ background: 'var(--bg)', color: 'var(--text)' }"
  >
    <div class="grid-overlay"></div>

    <div class="app-content">
      <!-- Navigation -->
      <header
        class="fixed top-0 left-0 w-full z-50"
        style="
          background: rgba(10, 10, 15, 0.85);
          backdrop-filter: blur(20px);
          border-bottom: 1px solid rgba(74, 222, 128, 0.08);
        "
      >
        <nav
          class="max-w-6xl mx-auto px-6 py-4 flex items-center justify-between"
        >
          <a
            href="#hero"
            class="font-mono text-lg font-semibold"
            :style="{ color: 'var(--accent)' }"
            @click.prevent="scrollToSection('hero')"
          >
            &lt;{{ initials }} /&gt;
          </a>

          <div class="hidden md:flex items-center gap-8">
            <a
              class="nav-link font-mono text-sm"
              :style="navLinkStyle"
              href="#about"
              @click.prevent="scrollToSection('about')"
              >about</a
            >
            <a
              class="nav-link font-mono text-sm"
              :style="navLinkStyle"
              href="#projects"
              @click.prevent="scrollToSection('projects')"
              >work</a
            >
            <a
              class="nav-link font-mono text-sm"
              :style="navLinkStyle"
              href="#skills"
              @click.prevent="scrollToSection('skills')"
              >skills</a
            >
            <a
              class="nav-link font-mono text-sm"
              :style="navLinkStyle"
              href="#contact"
              @click.prevent="scrollToSection('contact')"
              >contact</a
            >

            <div class="flex items-center gap-2">
              <div class="status-dot"></div>
              <span
                class="font-mono text-xs"
                :style="{ color: 'var(--accent)' }"
                >{{ config.statusText }}</span
              >
            </div>
          </div>

          <button
            class="md:hidden flex flex-col gap-1.5 p-2"
            aria-label="Toggle menu"
            style="background: none; border: none; cursor: pointer"
            @click="openMobileNav"
          >
            <span
              class="block w-6 h-0.5"
              :style="{ background: 'var(--text)' }"
            ></span>
            <span
              class="block w-4 h-0.5"
              :style="{ background: 'var(--accent)' }"
            ></span>
            <span
              class="block w-6 h-0.5"
              :style="{ background: 'var(--text)' }"
            ></span>
          </button>
        </nav>
      </header>

      <!-- Mobile Nav Overlay -->
      <div
        class="mobile-nav fixed inset-0 z-50 flex flex-col items-center justify-center gap-8"
        :class="{ open: mobileNavOpen }"
        :style="{
          background: 'rgba(10, 10, 15, 0.98)',
          display: mobileNavOpen ? 'flex' : 'none',
        }"
      >
        <button
          class="absolute top-6 right-6 text-2xl"
          style="
            background: none;
            border: none;
            color: var(--text);
            cursor: pointer;
          "
          aria-label="Close menu"
          @click="closeMobileNav"
        >
          ✕
        </button>

        <a
          class="font-mono text-xl"
          :style="mobileLinkStyle"
          href="#about"
          @click.prevent="mobileGo('about')"
          >about</a
        >
        <a
          class="font-mono text-xl"
          :style="mobileLinkStyle"
          href="#projects"
          @click.prevent="mobileGo('projects')"
          >work</a
        >
        <a
          class="font-mono text-xl"
          :style="mobileLinkStyle"
          href="#skills"
          @click.prevent="mobileGo('skills')"
          >skills</a
        >
        <a
          class="font-mono text-xl"
          :style="mobileLinkStyle"
          href="#contact"
          @click.prevent="mobileGo('contact')"
          >contact</a
        >
      </div>

      <main>
        <!-- Hero -->
        <section
          id="hero"
          class="hero-mesh relative flex items-center justify-center"
          style="min-height: 100%; padding: 120px 24px 80px"
        >
          <div class="relative z-10 max-w-4xl mx-auto text-center">
            <div
              class="reveal reveal-delay-1 font-mono text-sm mb-6 flex items-center justify-center gap-3"
              :style="{ color: 'var(--accent)' }"
            >
              <span :style="hrAccent"></span>
              Hello World, I'm
              <span :style="hrAccent"></span>
            </div>

            <h1
              class="reveal reveal-delay-2 font-bold tracking-tight mb-4"
              :style="heroNameStyle"
            >
              {{ config.heroName }}
            </h1>

            <p
              class="reveal reveal-delay-3 font-mono text-lg md:text-xl mb-4"
              :style="{ color: 'var(--accent2)' }"
            >
              {{ config.heroTitle }}
            </p>

            <p
              class="reveal reveal-delay-4 text-base md:text-lg max-w-xl mx-auto mb-10"
              :style="{ opacity: 0.6, lineHeight: '1.7' }"
            >
              {{ config.heroTagline }}
            </p>

            <div
              class="reveal reveal-delay-5 flex flex-wrap items-center justify-center gap-4"
            >
              <a
                href="#projects"
                class="cta-btn font-mono text-sm font-medium px-8 py-3 rounded-lg inline-block"
                :style="{
                  background: 'var(--accent)',
                  color: 'var(--bg)',
                  textDecoration: 'none',
                }"
                @click.prevent="scrollToSection('projects')"
              >
                Ver proyectos →
              </a>
              <a
                href="#contact"
                class="cta-btn font-mono text-sm font-medium px-8 py-3 rounded-lg inline-block"
                :style="{
                  background: 'transparent',
                  color: 'var(--accent)',
                  textDecoration: 'none',
                  border: '1px solid rgba(74, 222, 128, 0.3)',
                }"
                @click.prevent="scrollToSection('contact')"
              >
                Contactar
              </a>
            </div>
          </div>
        </section>

        <!-- About -->
        <section
          id="about"
          style="
            padding: 100px 24px;
            border-top: 1px solid rgba(74, 222, 128, 0.06);
          "
        >
          <div class="max-w-5xl mx-auto">
            <div class="flex items-center gap-4 mb-12 reveal">
              <span
                class="font-mono text-sm"
                :style="{ color: 'var(--accent)' }"
                >01.</span
              >
              <h2 class="text-2xl md:text-3xl font-bold">
                {{ config.aboutHeading }}
              </h2>
              <span
                style="
                  display: block;
                  flex: 1;
                  max-width: 200px;
                  height: 1px;
                  background: rgba(74, 222, 128, 0.15);
                "
              ></span>
            </div>

            <div class="grid md:grid-cols-5 gap-12 items-start">
              <div class="md:col-span-3 reveal reveal-delay-1">
                <p class="text-base leading-relaxed mb-6" style="opacity: 0.8">
                  {{ config.aboutText }}
                </p>
                <p class="text-base leading-relaxed" style="opacity: 0.6">
                  {{ config.aboutExtra }}
                </p>
              </div>

              <div class="md:col-span-2 reveal reveal-delay-2">
                <div
                  class="glow-border rounded-xl p-6"
                  :style="{ background: 'var(--surface)' }"
                >
                  <p
                    class="font-mono text-xs mb-4"
                    :style="{ color: 'var(--accent)' }"
                  >
                    // tech_stack.js
                  </p>
                  <div class="grid grid-cols-2 gap-2">
                    <span
                      v-for="(t, idx) in config.techStack"
                      :key="t"
                      class="tech-tag font-mono"
                      :style="idx % 2 === 0 ? techTagAccent : techTagAccent2"
                    >
                      {{ t }}
                    </span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <!-- Projects -->
        <section
          id="projects"
          style="
            padding: 100px 24px;
            border-top: 1px solid rgba(74, 222, 128, 0.06);
          "
        >
          <div class="max-w-5xl mx-auto">
            <div class="flex items-center gap-4 mb-12 reveal">
              <span
                class="font-mono text-sm"
                :style="{ color: 'var(--accent)' }"
                >02.</span
              >
              <h2 class="text-2xl md:text-3xl font-bold">
                {{ config.projectsHeading }}
              </h2>
              <span
                style="
                  display: block;
                  flex: 1;
                  max-width: 200px;
                  height: 1px;
                  background: rgba(74, 222, 128, 0.15);
                "
              ></span>
            </div>

            <div class="flex flex-col gap-8">
              <div
                v-for="(p, i) in projects"
                :key="p.title"
                class="glow-border rounded-xl overflow-hidden reveal"
                :class="`reveal-delay-${Math.min(i + 1, 5)}`"
                :style="{ background: 'var(--surface)' }"
              >
                <div class="grid md:grid-cols-2">
                  <!-- Visual -->
                  <div
                    class="project-visual flex items-center justify-center p-8"
                    :class="p.reverseOnDesktop ? 'order-1 md:order-2' : ''"
                    :style="p.visualStyle"
                  >
                    <!-- Si querés, acá podés meter img/screenshot real del proyecto -->
                    <div class="text-center">
                      <img
                        :src="p.image"
                        :alt="p.title"
                        class="w-full h-full object-cover"
                      />
                    </div>
                  </div>

                  <!-- Text -->
                  <div
                    class="p-8 flex flex-col justify-center"
                    :class="p.reverseOnDesktop ? 'order-2 md:order-1' : ''"
                  >
                    <span
                      class="font-mono text-xs mb-2"
                      :style="{ color: p.accent }"
                      >Proyecto</span
                    >
                    <h3 class="text-xl font-bold mb-3">{{ p.title }}</h3>
                    <p
                      class="text-sm mb-4"
                      style="opacity: 0.6; line-height: 1.7"
                    >
                      {{ p.description }}
                    </p>

                    <div class="flex flex-wrap gap-2 mb-4">
                      <span
                        v-for="tag in p.tags"
                        :key="tag"
                        class="tech-tag font-mono"
                        :style="p.tagStyle"
                      >
                        {{ tag }}
                      </span>
                    </div>

                    <div class="flex gap-4 flex-wrap">
                      <a
                        v-if="p.liveUrl"
                        class="font-mono text-xs cursor-pointer"
                        :style="{ color: p.accent, textDecoration: 'none' }"
                        :href="p.liveUrl"
                        target="_blank"
                        rel="noopener noreferrer"
                        >↗ Live Demo</a
                      >

                      <a
                        v-if="p.repoUrl"
                        class="font-mono text-xs cursor-pointer"
                        :style="{
                          color: 'var(--text)',
                          opacity: 0.5,
                          textDecoration: 'none',
                        }"
                        :href="p.repoUrl"
                        target="_blank"
                        rel="noopener noreferrer"
                        >↗ GitHub</a
                      >
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </section>

        <!-- Skills -->
        <section
          id="skills"
          style="
            padding: 100px 24px;
            border-top: 1px solid rgba(74, 222, 128, 0.06);
          "
        >
          <div class="max-w-5xl mx-auto">
            <div class="flex items-center gap-4 mb-12 reveal">
              <span
                class="font-mono text-sm"
                :style="{ color: 'var(--accent)' }"
                >03.</span
              >
              <h2 class="text-2xl md:text-3xl font-bold">
                {{ config.skillsHeading }}
              </h2>
              <span
                style="
                  display: block;
                  flex: 1;
                  max-width: 200px;
                  height: 1px;
                  background: rgba(74, 222, 128, 0.15);
                "
              ></span>
            </div>

            <div class="grid md:grid-cols-2 gap-8">
              <!-- Frontend -->
              <div
                class="glow-border rounded-xl p-6 reveal reveal-delay-1"
                :style="{ background: 'var(--surface)' }"
              >
                <h3
                  class="font-mono text-sm mb-6"
                  :style="{ color: 'var(--accent)' }"
                >
                  Frontend
                </h3>

                <div class="flex flex-col gap-4">
                  <div v-for="s in skills.frontend" :key="s.name">
                    <div class="flex justify-between mb-1">
                      <span class="text-sm">{{ s.name }}</span>
                      <span
                        class="font-mono text-xs"
                        :style="{ color: 'var(--accent)' }"
                        >{{ s.level }}%</span
                      >
                    </div>
                    <div
                      style="
                        height: 4px;
                        background: rgba(74, 222, 128, 0.1);
                        border-radius: 2px;
                      "
                    >
                      <div
                        class="skill-fill"
                        :style="{
                          '--skill-width': s.level + '%',
                          background:
                            'linear-gradient(90deg, var(--accent), var(--accent2))',
                        }"
                      />
                    </div>
                  </div>
                </div>
              </div>

              <!-- Backend -->
              <div
                class="glow-border rounded-xl p-6 reveal reveal-delay-2"
                :style="{ background: 'var(--surface)' }"
              >
                <h3
                  class="font-mono text-sm mb-6"
                  :style="{ color: 'var(--accent2)' }"
                >
                  Backend
                </h3>

                <div class="flex flex-col gap-4">
                  <div v-for="s in skills.backend" :key="s.name">
                    <div class="flex justify-between mb-1">
                      <span class="text-sm">{{ s.name }}</span>
                      <span
                        class="font-mono text-xs"
                        :style="{ color: 'var(--accent2)' }"
                        >{{ s.level }}%</span
                      >
                    </div>
                    <div
                      style="
                        height: 4px;
                        background: rgba(99, 102, 241, 0.1);
                        border-radius: 2px;
                      "
                    >
                      <div
                        class="skill-fill"
                        :style="{
                          '--skill-width': s.level + '%',
                          background:
                            'linear-gradient(90deg, var(--accent2), var(--accent))',
                        }"
                      />
                    </div>
                  </div>
                </div>
              </div>

              <!-- DevOps -->
              <div
                class="glow-border rounded-xl p-6 reveal reveal-delay-3"
                :style="{ background: 'var(--surface)' }"
              >
                <h3
                  class="font-mono text-sm mb-6"
                  :style="{ color: 'var(--accent)' }"
                >
                  DevOps & Tools
                </h3>
                <div class="flex flex-wrap gap-2">
                  <span
                    v-for="t in skills.devops"
                    :key="t"
                    class="tech-tag font-mono"
                    :style="techTagAccent"
                  >
                    {{ t }}
                  </span>
                </div>
              </div>

              <!-- Soft Skills -->
              <div
                class="glow-border rounded-xl p-6 reveal reveal-delay-4"
                :style="{ background: 'var(--surface)' }"
              >
                <h3
                  class="font-mono text-sm mb-6"
                  :style="{ color: 'var(--accent2)' }"
                >
                  Soft Skills
                </h3>
                <div class="flex flex-wrap gap-2">
                  <span
                    v-for="t in skills.soft"
                    :key="t"
                    class="tech-tag font-mono"
                    :style="techTagAccent2"
                  >
                    {{ t }}
                  </span>
                </div>
              </div>
            </div>
          </div>
        </section>

        <!-- Contact -->
        <section
          id="contact"
          style="
            padding: 100px 24px 60px;
            border-top: 1px solid rgba(74, 222, 128, 0.06);
          "
        >
          <div class="max-w-3xl mx-auto text-center">
            <div class="flex items-center justify-center gap-4 mb-6 reveal">
              <span
                class="font-mono text-sm"
                :style="{ color: 'var(--accent)' }"
                >04.</span
              >
              <h2 class="text-2xl md:text-3xl font-bold">
                {{ config.contactHeading }}
              </h2>
            </div>

            <p
              class="text-base mb-10 reveal reveal-delay-1"
              style="
                opacity: 0.6;
                max-width: 500px;
                margin: 0 auto 40px;
                line-height: 1.7;
              "
            >
              {{ config.contactText }}
            </p>

            <form
              name="contact"
              method="POST"
              data-netlify="true"
              netlify-honeypot="bot-field"
              class="glow-border rounded-xl p-8 text-left reveal reveal-delay-2"
              :style="{ background: 'var(--surface)' }"
              @submit.prevent="submitForm"
            >
              <!-- Netlify requiere esto -->
              <input type="hidden" name="form-name" value="contact" />

              <!-- Honeypot anti-spam -->
              <p class="hidden">
                <label>Don’t fill this out: <input name="bot-field" /></label>
              </p>

              <div class="grid md:grid-cols-2 gap-6 mb-6">
                <div>
                  <label
                    class="font-mono text-xs mb-2 block"
                    :style="{ color: 'var(--accent)' }"
                  >
                    Nombre
                  </label>
                  <input
                    v-model.trim="form.name"
                    name="name"
                    type="text"
                    placeholder="Tu nombre"
                    class="form-input w-full px-4 py-3 rounded-lg font-primary text-sm"
                    :style="inputStyle"
                  />
                </div>

                <div>
                  <label
                    class="font-mono text-xs mb-2 block"
                    :style="{ color: 'var(--accent)' }"
                  >
                    Email
                  </label>
                  <input
                    v-model.trim="form.email"
                    name="email"
                    type="email"
                    placeholder="tu@email.com"
                    class="form-input w-full px-4 py-3 rounded-lg font-primary text-sm"
                    :style="inputStyle"
                  />
                </div>
              </div>

              <div class="mb-6">
                <label
                  class="font-mono text-xs mb-2 block"
                  :style="{ color: 'var(--accent)' }"
                >
                  Mensaje
                </label>
                <textarea
                  v-model.trim="form.message"
                  name="message"
                  rows="4"
                  placeholder="Cuéntame sobre tu proyecto..."
                  class="form-input w-full px-4 py-3 rounded-lg font-primary text-sm resize-none"
                  :style="inputStyle"
                />
              </div>

              <button
                type="submit"
                class="cta-btn font-mono text-sm font-medium px-8 py-3 rounded-lg w-full"
                :disabled="sending"
                :style="{
                  background: 'var(--accent)',
                  color: 'var(--bg)',
                  border: 'none',
                  cursor: 'pointer',
                  opacity: sending ? 0.6 : 1,
                }"
              >
                {{ sending ? "Enviando..." : "Enviar mensaje →" }}
              </button>

              <div
                v-if="feedback.show"
                class="mt-4 text-center text-sm font-mono"
              >
                <span :style="{ color: feedback.color }">{{
                  feedback.text
                }}</span>
              </div>
            </form>

            <div
              class="flex items-center justify-center gap-8 mt-12 reveal reveal-delay-3"
            >
              <a
                v-for="l in links"
                :key="l.label"
                class="font-mono text-sm nav-link"
                :style="{
                  color: 'var(--text)',
                  opacity: 0.5,
                  textDecoration: 'none',
                }"
                :href="l.url"
                target="_blank"
                rel="noopener noreferrer"
                >{{ l.label }}</a
              >
            </div>

            <p
              class="font-mono text-xs mt-8 reveal reveal-delay-4"
              style="opacity: 0.3"
            >
              {{ config.contactEmail }}
            </p>
          </div>
        </section>
      </main>

      <footer
        style="
          padding: 30px 24px;
          border-top: 1px solid rgba(74, 222, 128, 0.06);
          text-align: center;
        "
      >
        <p class="font-mono text-xs" style="opacity: 0.25">
          {{ new Date().getFullYear() }}
        </p>
      </footer>
    </div>
  </div>
</template>

<script setup>
import {
  computed,
  onMounted,
  onBeforeUnmount,
  reactive,
  ref,
  nextTick,
} from "vue";

const appWrapper = ref(null);
const mobileNavOpen = ref(false);

const config = reactive({
  heroName: "Gabriel Casas",
  heroTitle: "Full-Stack Developer",
  heroTagline:
    "Construyo aplicaciones web modernas y prácticas. Me enfoco en resolver necesidades reales con código claro y buen UX.",
  statusText: "Disponible",

  aboutHeading: "Sobre mí",
  aboutText:
    "Soy desarrollador Full-Stack especializado en crear herramientas que optimizan la gestión de negocios. Tengo experiencia trabajando mano a mano con emprendimientos reales, traduciendo necesidades operativas en sistemas web robustos y escalables.",
  aboutExtra:
    "Disfruto trabajar en proyectos donde el software tiene impacto directo en la operación diaria y ayuda a mejorar procesos reales.",

  techStack: [
    "Vue",
    "Django",
    "JavaScript",
    "Python",
    "Node.js",
    "PostgreSQL",
    "Git",
    "Tailwind",
  ],

  projectsHeading: "Proyectos destacados",
  skillsHeading: "Habilidades",

  contactHeading: "¿Trabajamos juntos?",
  contactText:
    "Estoy abierto a oportunidades junior, proyectos freelance y colaboraciones. Si te interesa mi perfil, escribime.",
  contactEmail: "gcasas132@gmail.com",
});

const projects = reactive([
  {
    title:
      "Alma Pastelería — Sistema de gestión interna (Tesis / Cliente real)",
    description:
      "Sistema web full-stack para una pastelería real. Incluye gestión de insumos, recetas y pedidos, control de stock mínimo y reportes operativos para seguimiento diario.",
    tags: ["Vue 3", "Vite", "Django", "DRF", "PostgreSQL"],
    accent: "var(--accent)",
    tagStyle: {
      background: "rgba(74, 222, 128, 0.08)",
      color: "var(--accent)",
    },
    image: "/img/alma-demo.png",
    visualLabel: "FULLSTACK APP",
    visualStyle: {
      background:
        "linear-gradient(135deg, rgba(74, 222, 128, 0.05), rgba(99, 102, 241, 0.05))",
      minHeight: "220px",
    },
    liveUrl: "https://comforting-maamoul-b375a3.netlify.app", // si algún día lo deployás, lo ponés acá
    repoUrl: "https://github.com/Gabriel0511/almaPasteleria",
    reverseOnDesktop: false,
  },
  {
    title: "Merakii — Ecommerce para emprendimiento de lencería",
    description:
      "Ecommerce desarrollado para un emprendimiento real. Estructura lista para catálogo, páginas de producto y experiencia mobile-first. (Actualmente sin productos por baja temporal del cliente).",
    tags: ["Vue 3", "Vite", "UI/UX", "Responsive"],
    accent: "var(--accent2)",
    tagStyle: {
      background: "rgba(99, 102, 241, 0.08)",
      color: "var(--accent2)",
    },
    image: "/img/meraki-demo.png",
    visualLabel: "ECOMMERCE",
    visualStyle: {
      background:
        "linear-gradient(135deg, rgba(99, 102, 241, 0.05), rgba(74, 222, 128, 0.05))",
      minHeight: "220px",
    },
    liveUrl: "https://merakii.com.ar/",
    repoUrl: "", // cuando lo subas
    reverseOnDesktop: true,
  },
  {
    title: "Landing profesional — Estudio contable",
    description:
      "Landing page institucional orientada a presentación de servicios y contacto. Diseño claro, responsive y preparada para campañas de captación.",
    tags: ["Vue 3", "Vite", "Landing", "Responsive"],
    accent: "var(--accent)",
    tagStyle: {
      background: "rgba(74, 222, 128, 0.08)",
      color: "var(--accent)",
    },
    image: "/img/landing-demo.png",
    visualLabel: "LANDING",
    visualStyle: {
      background:
        "linear-gradient(135deg, rgba(74, 222, 128, 0.05), rgba(99, 102, 241, 0.05))",
      minHeight: "220px",
    },
    liveUrl: "https://spiffy-lokum-e1aeea.netlify.app/",
    repoUrl: "",
    reverseOnDesktop: false,
  },
  {
    title: "Sistema de matrículas — Instituto (Proyecto académico)",
    description:
      "Frontend para gestión de matrículas: flujo de inscripción, validaciones y pantallas administrativas. Proyecto académico (sin persistencia de datos).",
    tags: ["Vue 3", "Vite", "Frontend"],
    accent: "var(--accent2)",
    tagStyle: {
      background: "rgba(99, 102, 241, 0.08)",
      color: "var(--accent2)",
    },
    image: "/img/matricula-demo.png",
    visualLabel: "FRONTEND",
    visualStyle: {
      background:
        "linear-gradient(135deg, rgba(99, 102, 241, 0.05), rgba(74, 222, 128, 0.05))",
      minHeight: "220px",
    },
    liveUrl: "https://gestionitsc.netlify.app/",
    repoUrl: "",
    reverseOnDesktop: true,
  },
]);

const skills = reactive({
  frontend: [
    { name: "Vue / Vite", level: 85 },
    { name: "JavaScript", level: 80 },
    { name: "CSS / Tailwind", level: 80 },
  ],
  backend: [
    { name: "Python / Django", level: 80 },
    { name: "Node.js / Express", level: 70 },
    { name: "SQL (PostgreSQL/MySQL)", level: 85 },
  ],
  devops: ["Git/GitHub", "Linux", "Docker (básico)", "CI/CD (básico)"],
  soft: [
    "Comunicación",
    "Aprendizaje rápido",
    "Resolución de problemas",
    "Responsabilidad",
  ],
});

const links = reactive([
  { label: "GitHub", url: "https://github.com/Gabriel0511" },
  {
    label: "LinkedIn",
    url: "https://www.linkedin.com/in/gabriel-casas-9a5a5a207/",
  },
  { label: "Portfolio", url: "#" },
]);

const initials = computed(() =>
  config.heroName
    .split(" ")
    .filter(Boolean)
    .map((p) => p[0].toUpperCase())
    .join(""),
);

const navLinkStyle = {
  color: "var(--text)",
  opacity: 0.7,
  textDecoration: "none",
};
const mobileLinkStyle = { color: "var(--text)", textDecoration: "none" };

const hrAccent = {
  display: "inline-block",
  width: "40px",
  height: "1px",
  background: "var(--accent)",
};
const heroNameStyle = {
  fontSize: "clamp(2.5rem, 6vw, 5rem)",
  lineHeight: 1.05,
};

const decorLeftStyle = {
  color: "var(--accent)",
  opacity: 0.15,
  animation: "meshFloat 15s ease-in-out infinite",
};
const decorRightStyle = {
  color: "var(--accent2)",
  opacity: 0.15,
  animation: "meshFloat 18s ease-in-out infinite reverse",
};

const techTagAccent = {
  background: "rgba(74, 222, 128, 0.08)",
  color: "var(--accent)",
};
const techTagAccent2 = {
  background: "rgba(99, 102, 241, 0.08)",
  color: "var(--accent2)",
};

const inputStyle = {
  background: "rgba(74, 222, 128, 0.03)",
  border: "1px solid rgba(74, 222, 128, 0.1)",
  color: "var(--text)",
};

function openMobileNav() {
  mobileNavOpen.value = true;
}
function closeMobileNav() {
  mobileNavOpen.value = false;
}
function mobileGo(id) {
  closeMobileNav();
  scrollToSection(id);
}

function scrollToSection(id) {
  const target = document.getElementById(id);
  if (!target) return;

  target.scrollIntoView({ behavior: "smooth", block: "start" });
}

/** Reveal + skill anim */
let observer = null;

onMounted(() => {
  // trigger initial reveal hero
  setTimeout(() => {
    document
      .querySelectorAll("#hero .reveal")
      .forEach((el) => el.classList.add("visible"));
  }, 200);

  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (!entry.isIntersecting) return;

        entry.target.classList.add("visible");

        // animate skill bars inside the revealed block
        entry.target.querySelectorAll(".skill-fill").forEach((bar) => {
          setTimeout(() => bar.classList.add("animate"), 300);
        });
      });
    },
    { threshold: 0.1, rootMargin: "0px 0px -50px 0px" },
  );

  document.querySelectorAll(".reveal").forEach((el) => observer.observe(el));
});

onBeforeUnmount(() => {
  if (observer) observer.disconnect();
});

/** Contact form */
const form = reactive({ name: "", email: "", message: "" });
const sending = ref(false);
const feedback = reactive({ show: false, text: "", color: "var(--accent)" });

function showFeedback(text, color) {
  feedback.show = true;
  feedback.text = text;
  feedback.color = color;
  setTimeout(() => (feedback.show = false), 4000);
}

function encodeForm(data) {
  return Object.keys(data)
    .map((k) => encodeURIComponent(k) + "=" + encodeURIComponent(data[k]))
    .join("&");
}

async function submitForm() {
  if (!form.name || !form.email || !form.message) {
    showFeedback("⚠ Por favor completa todos los campos", "#fbbf24");
    return;
  }

  sending.value = true;

  try {
    await fetch("/", {
      method: "POST",
      headers: { "Content-Type": "application/x-www-form-urlencoded" },
      body: encodeForm({
        "form-name": "contact",
        name: form.name,
        email: form.email,
        message: form.message,
      }),
    });

    showFeedback("✓ ¡Mensaje enviado! Te responderé pronto.", "var(--accent)");
    form.name = "";
    form.email = "";
    form.message = "";
  } catch (e) {
    showFeedback("❌ Error al enviar. Probá de nuevo.", "#f87171");
  } finally {
    sending.value = false;
  }
}
</script>
