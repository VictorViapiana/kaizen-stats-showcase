# 🎮 Kaizen Stats API & 3D Showcase (Full-Stack)

> 🔒 **Note:** This is a Showcase repository. The source code for this project is private and commercially owned. This page serves to demonstrate the software architecture, the technologies used, and the developed user interface.

## 🎯 Overview
This project is an advanced Full-Stack Web Application built to connect a game server's internal database to a public-facing web interface. It allows users to query player statistics in real-time while dynamically rendering the player's in-game avatar in a fully interactive 3D environment.

Unlike simple stat-checkers, this platform was engineered to handle asynchronous external API calls (fetching official skins and capes), prevent WebGL memory leaks on mobile devices, and ensure high-performance database querying without deadlocking the main server threads.

<video src="./Kaizen-stats.mp4" autoplay loop muted playsinline width="100%"></video>

---

## 🛠️ Technologies Used
* **Python (FastAPI)** – High-performance asynchronous backend and RESTful API creation.
* **MySQL** – Relational database management for instantaneous player statistics retrieval.
* **JavaScript (Vanilla) & WebGL** – Frontend business logic, asynchronous data fetching (`fetch` API), and 3D rendering engine (`skinview3d`).
* **HTML5 & Advanced CSS3** – Responsive UI/UX design, Flexbox/Grid layouts, and immersive visual effects (tsParticles).

---

## 📊 Architecture & Data Flow (The Pipeline)
The system executes a highly optimized, non-blocking execution flow:
1. **Client Request:** The user inputs a nickname. The frontend intercepts the request and communicates asynchronously with the local Python API.
2. **Database Querying:** The backend securely connects to the MySQL database, fetching win streaks and match history using parameterized queries to prevent SQL Injection.
3. **External API Orchestration:** Simultaneously, the backend routes requests to external servers (OptiFine and Mojang API) to locate the player's official cape/textures.
4. **Smart Caching:** Successfully retrieved capes are cached in the backend memory, drastically reducing response times for repeated queries and avoiding rate-limiting from external APIs.
5. **Dynamic 3D Rendering:** The JavaScript engine receives the JSON payload, clears any existing WebGL context to prevent mobile memory crashes, and renders the 3D model with the custom cape and walking animations applied.

---

## 💻 User Interface & 3D Output
The frontend was designed focusing on a modern, gaming-oriented aesthetic with high usability:
* **Immersive Visual Identity:** Custom dark-theme background with interactive purple neon particles (`#06020E` to `#A855F7` transitions) providing a premium feel.
* **Real-Time 3D Engine:** Fully interactive 3D skin viewer mapped to an HTML Canvas, allowing users to rotate and inspect the player's avatar.
* **Mobile-First Responsiveness:** Fluid layout structuring that adapts seamlessly to desktop monitors and smartphone screens without breaking the canvas aspect ratio.

---

## 🧠 Key Features & Optimizations
* **WebGL Memory Management:** Implemented strict disposal routines (`dispose()`) for the 3D viewer to prevent rendering queue crashes and browser memory leaks (WebGL context limits), especially on low-end mobile devices.
* **Backend Deadlock Prevention:** Robust database connection handling (`try...finally` blocks) and timeout configurations on external `httpx` requests, ensuring the server never hangs.
* **Asynchronous Concurrency:** Full reliance on `async/await` in both Python and JavaScript, maximizing throughput and non-blocking I/O operations.
* **API Fallback System:** Intelligent routing that attempts to fetch cosmetic data from multiple sources (Optifine -> Mojang Session Servers), gracefully failing without breaking the user experience.

---

## 📁 Project Structure (Conceptual)
    kaizen_stats_platform/
    ├── backend/
    │   ├── main.py                # FastAPI core, routing, and Cache system
    │   ├── database.py            # MySQL connection pooling and queries
    │   └── requirements.txt       # Backend dependencies (fastapi, uvicorn, httpx, pymysql)
    ├── frontend/
    │   ├── index.html             # UI Structure and Canvas container
    │   ├── style.css              # Styling, animations, and responsive grids
    │   └── script.js              # DOM manipulation, Fetch API, and WebGL rendering
    └── README.md                  # Project documentation

---

## 🚀 Project Goal
This project was engineered to demonstrate high-level Full-Stack capabilities, transitioning from static web pages to dynamic, real-time web applications. It highlights strict architectural patterns, advanced API consumption, memory management in the browser, and secure database interactions.

---

## 🤝 Contributing
Contributions, issues, and feature requests are welcome! Feel free to check the issues page.

---

## 📎 Author
Developed by **Victor Viapiana**

* **GitHub:** [https://github.com/VictorViapiana](https://github.com/VictorViapiana)
