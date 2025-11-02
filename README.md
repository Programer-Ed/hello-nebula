# 🌌 Hello Nebula

> A creative twist on the classic “Hello World” — reimagined as an interactive, animated, and expressive micro-app built with **Vue 3 + TypeScript**.

Users can personalize their greeting, set their mood, and pick an emoji while the background comes alive with a **dynamic starfield**, **floating gradients**, and **smooth parallax motion**.

✨ Triple-tap the title for a confetti explosion, toggle between light/dark themes, and enjoy subtle animations powered by **pure CSS** and a touch of **canvas magic**.

It’s not just “Hello World.”  
It’s **“Hello, Universe.”**

---

## 🚀 Features

- 🪄 **Personalized greeting** — Your name appears dynamically in the title.  
- 😄 **Mood field** — Express how you’re feeling today.  
- 🎭 **Emoji selector** — Choose an emoji that fits your vibe.  
- 🎉 **Triple-tap confetti** — Celebrate with a burst of color!  
- 🌗 **Light/Dark theme toggle** — Smooth transitions with style.  
- 🌠 **Animated starfield** — Dynamic, parallax background using Canvas.  
- 🎨 **Responsive design** — Looks stunning across all screens.

---

## 🛠️ Technologies Used

- [Vue 3](https://vuejs.org/) – reactive frontend framework  
- [TypeScript](https://www.typescriptlang.org/) – type-safe logic  
- [Vite](https://vitejs.dev/) – fast development build tool  
- [Canvas API](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API) – starfield rendering  
- [CSS3 Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations) – transitions and glow effects  
- [canvas-confetti](https://www.npmjs.com/package/canvas-confetti) – for party mode  

---

## 💻 Installation

### Prerequisites
- Node.js (>= 18)
- npm 

### Setup

```bash
# clone the repo
git clone https://github.com/Programer-Ed/hello-nebula.git

cd hello-nebula

# install dependencies
npm install

# start dev server

npm run dev
````

Then open your browser and navigate to:
👉 `http://localhost:5173`

---

## 🧭 Usage

1. Type your **name** and **mood**.
2. Choose an **emoji** that matches your energy.
3. Click the title three times to unleash **confetti magic**!
4. Toggle between **light/dark mode**.
5. Move your mouse to see the **interactive starfield** respond.

---

## ⚙️ Configuration Options

You can tweak small parts of the app in `App.vue`:

| Option      | Description                   | Default                                      |
| ----------- | ----------------------------- | -------------------------------------------- |
| `hellos`    | List of greetings that rotate | `["Hello", "Hola", "Bonjour", "こんにちは", ...]` |
| `particles` | Star count in background      | `100`                                        |
| `accent`    | Accent color per theme        | light: `#6a5acd`, dark: `#00bcd4`            |

---

## 🧩 Project Structure

```
hello-nebula/
│
├── public/
│   └── favicon.ico
│
├── src/
│   ├── assets/           # Images, icons
│   ├── components/       # Vue components (optional)
│   ├── App.vue           # Main UI with starfield + inputs
│   ├── main.ts           # Entry point
│   └── styles.css        # Base styles (if extracted)
│
├── index.html
├── package.json
└── vite.config.ts
```

---

## 🧰 Troubleshooting

**App doesn’t start / blank screen**

* Make sure you installed dependencies correctly.
* Run `pnpm run dev` (not just `pnpm dev`).

**Canvas not full-screen**

* Ensure your `.app` container uses `height: 100vh; width: 100vw;`.

**Confetti not working**

* Check browser console for errors.
* Ensure `canvas-confetti` is installed.

---

## 🤝 Contributing

Pull requests are welcome!
If you’d like to contribute:

1. Fork the repo
2. Create a new branch: `git checkout -b feature/your-feature`
3. Commit your changes
4. Push and open a PR 🚀

---

## 📜 License

This project is licensed under the **MIT License** — free to modify, remix, and explore.

