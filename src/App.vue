<template>
  <div :class="['app', theme]">
    <canvas ref="stars" class="stars"></canvas>

    <div
      class="gradient-bg"
      :style="{
        background: `radial-gradient(circle at ${mouse.x}% ${mouse.y}%, var(--accent), transparent 70%)`
      }"
    ></div>

    <main class="content">
      <h1 class="title" @click="handleClick">
        {{ greeting }} {{ selectedEmoji }}
      </h1>

      <p class="hint">💡 Triple-tap the title for confetti magic 🎉</p>

      <div class="input-group">
        <input
          class="input"
          v-model="name"
          type="text"
          placeholder="👋 Type your name..."
        />
        <input
          class="input"
          v-model="mood"
          type="text"
          placeholder="😄 How are you feeling today?"
        />

        <select class="emoji-picker" v-model="selectedEmoji">
          <option disabled value="">✨ Pick an emoji ✨</option>
          <option v-for="emoji in emojis" :key="emoji" :value="emoji">
            {{ emoji }}
          </option>
        </select>
      </div>

      <p v-if="mood" class="mood-line">
        {{ moodEmoji }} Feeling <strong>{{ mood }}</strong> {{ selectedEmoji }}
      </p>

      <button class="toggle-btn" @click="toggleTheme">
        Toggle {{ theme === 'light' ? '🌙' : '☀️' }}
      </button>
    </main>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from "vue";
import confetti from "canvas-confetti";

const hellos = ["Hello", "Hola", "Bonjour", "こんにちは", "안녕", "Ciao", "नमस्ते", "مرحبا", "Olá"];
const hello = ref(hellos[0]);
const name = ref("");
const mood = ref("");
const selectedEmoji = ref("");
const emojis = ["🌈", "🔥", "💫", "🦋", "🧠", "🌻", "🎧", "🚀", "🍀", "✨", "🌸", "🎨", "💻", "🦄"];
const theme = ref<"light" | "dark">("light");
const mouse = ref({ x: 50, y: 50 });
const clicks = ref(0);

onMounted(() => {
  const interval = setInterval(() => {
    const i = (hellos.indexOf(hello.value) + 1) % hellos.length;
    hello.value = hellos[i];
  }, 2500);

  const handleMove = (e: MouseEvent) => {
    mouse.value = {
      x: (e.clientX / window.innerWidth) * 100,
      y: (e.clientY / window.innerHeight) * 100,
    };
  };

  window.addEventListener("mousemove", handleMove);
  drawStars();

  onUnmounted(() => {
    clearInterval(interval);
    window.removeEventListener("mousemove", handleMove);
  });
});

const greeting = computed(() => `${hello.value}, ${name.value || "World"} 🌍`);

const moodEmoji = computed(() => {
  const moods: Record<string, string> = {
    happy: "😄",
    sad: "😢",
    tired: "🥱",
    excited: "🤩",
    chill: "😎",
    angry: "😤",
    nervous: "😬",
    relaxed: "🧘‍♂️",
  };
  const key = Object.keys(moods).find((m) =>
    mood.value.toLowerCase().includes(m)
  );
  return key ? moods[key] : "🌈";
});

const toggleTheme = () => {
  theme.value = theme.value === "light" ? "dark" : "light";
};

const handleClick = () => {
  clicks.value++;
  if (clicks.value >= 3) {
    confetti({ particleCount: 80, spread: 70, origin: { y: 0.6 } });
    clicks.value = 0;
  }
};

// 🎇 Starfield
const stars = ref<HTMLCanvasElement | null>(null);
function drawStars() {
  const canvas = stars.value!;
  const ctx = canvas.getContext("2d")!;
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  const particles = Array.from({ length: 100 }, () => ({
    x: Math.random() * canvas.width,
    y: Math.random() * canvas.height,
    r: Math.random() * 1.5,
    s: Math.random() * 0.5 + 0.2,
  }));

  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = "white";
    particles.forEach((p) => {
      ctx.beginPath();
      ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
      ctx.fill();
      p.y += p.s;
      if (p.y > canvas.height) p.y = 0;
    });
    requestAnimationFrame(animate);
  }
  animate();
}

</script>

<style scoped>
:root {
  --accent: #6a5acd;
  --bg-light: #f9f9ff;
  --bg-dark: #0a0a10;
  --text-light: #1a1a2e;
  --text-dark: #fafaff;
}

.app {
  position: relative;
  height: 100vh;
  width: 100vw;
  overflow: hidden;
  transition: background 0.6s, color 0.6s;
  display: flex;
  align-items: center;
  justify-content: center;
}

.app.light {
  background: var(--bg-light);
  color: var(--text-light);
  --accent: #6a5acd;
}

.app.dark {
  background: var(--bg-dark);
  color: var(--text-dark);
  --accent: #00bcd4;
}

.gradient-bg {
  position: absolute;
  inset: 0;
  opacity: 0.3;
  pointer-events: none;
  transition: background 0.3s ease;
}

.stars {
  position: absolute;
  inset: 0;
  z-index: 0;
}

.content {
  z-index: 2;
  text-align: center;
  animation: fadeIn 1.2s ease;
}

.title {
  font-family: "Poppins", sans-serif;
  font-size: 3rem;
  margin-bottom: 0.5rem;
  cursor: pointer;
  text-shadow: 0 0 15px var(--accent);
  animation: glow 2s ease-in-out infinite alternate;
}

.hint {
  font-size: 0.9rem;
  opacity: 0.8;
  margin-bottom: 1.5rem;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 0.7rem;
  align-items: center;
}

.input,
.emoji-picker {
  padding: 0.6rem 1rem;
  border: 2px solid var(--accent);
  border-radius: 10px;
  background: transparent;
  color: inherit;
  font-size: 1rem;
  outline: none;
  transition: border-color 0.3s;
}

.emoji-picker {
  cursor: pointer;
  text-align: center;
}

.mood-line {
  margin-top: 1rem;
  font-size: 1.2rem;
  animation: fadeIn 1.5s ease;
}

.toggle-btn {
  margin-top: 1.5rem;
  padding: 0.7rem 1.2rem;
  font-size: 1rem;
  background: var(--accent);
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: transform 0.2s ease, background 0.3s ease;
}

.toggle-btn:hover {
  transform: scale(1.05);
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes glow {
  from {
    text-shadow: 0 0 10px var(--accent);
  }
  to {
    text-shadow: 0 0 25px var(--accent);
  }
}
</style>
