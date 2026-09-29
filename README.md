<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>GymTrack - Workout Planner</title>

  <style>
    :root {
      --bg: #f4f6f8;
      --card: #ffffff;
      --card-2: #f8fafc;
      --text: #111827;
      --muted: #6b7280;
      --border: #e5e7eb;
      --primary: #6366f1;
      --primary-dark: #4f46e5;
      --success: #10b981;
      --danger: #ef4444;
      --warning: #f59e0b;
      --shadow: 0 8px 30px rgba(15, 23, 42, 0.08);
      --radius: 16px;
    }

    body.dark {
      --bg: #0f172a;
      --card: #1e293b;
      --card-2: #172033;
      --text: #f8fafc;
      --muted: #94a3b8;
      --border: #334155;
      --shadow: 0 8px 30px rgba(0, 0, 0, 0.25);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: Inter, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background: var(--bg);
      color: var(--text);
      min-height: 100vh;
      transition: background 0.25s, color 0.25s;
    }

    button,
    input,
    select,
    textarea {
      font: inherit;
    }

    button {
      cursor: pointer;
    }

    .app {
      display: flex;
      min-height: 100vh;
    }

    /* SIDEBAR */
    .sidebar {
      width: 250px;
      background: var(--card);
      border-right: 1px solid var(--border);
      padding: 24px 16px;
      position: fixed;
      left: 0;
      top: 0;
      bottom: 0;
      z-index: 100;
      display: flex;
      flex-direction: column;
    }

    .logo {
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 22px;
      font-weight: 800;
      padding: 8px 10px 28px;
    }

    .logo-icon {
      width: 40px;
      height: 40px;
      border-radius: 12px;
      background: linear-gradient(135deg, var(--primary), #8b5cf6);
      color: white;
      display: grid;
      place-items: center;
      font-size: 21px;
    }

    .nav {
      display: flex;
      flex-direction: column;
      gap: 6px;
    }

    .nav button {
      border: 0;
      background: transparent;
      color: var(--muted);
      padding: 13px 14px;
      border-radius: 12px;
      text-align: left;
      display: flex;
      align-items: center;
      gap: 12px;
      font-weight: 600;
      transition: 0.2s;
    }

    .nav button:hover,
    .nav button.active {
      background: rgba(99, 102, 241, 0.1);
      color: var(--primary);
    }

    .sidebar-bottom {
      margin-top: auto;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    /* MAIN */
    .main {
      margin-left: 250px;
      width: calc(100% - 250px);
      padding: 28px;
      max-width: 1600px;
    }

    .topbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 28px;
      gap: 15px;
    }

    .topbar h1 {
      font-size: 30px;
      margin-bottom: 5px;
    }

    .topbar p {
      color: var(--muted);
    }

    .top-actions {
      display: flex;
      gap: 10px;
    }

    /* BUTTONS */
    .btn {
      border: 1px solid var(--border);
      background: var(--card);
      color: var(--text);
      padding: 10px 15px;
      border-radius: 10px;
      font-weight: 700;
      transition: 0.2s;
    }

    .btn:hover {
      transform: translateY(-1px);
    }

    .btn-primary {
      background: var(--primary);
      color: white;
      border-color: var(--primary);
    }

    .btn-primary:hover {
      background: var(--primary-dark);
    }

    .btn-danger {
      color: var(--danger);
      border-color: var(--danger);
    }

    .btn-success {
      background: var(--success);
      color: white;
      border-color: var(--success);
    }

    .btn-small {
      padding: 7px 10px;
      font-size: 13px;
    }

    /* SECTIONS & GRIDS */
    .section {
      display: none;
    }

    .section.active {
      display: block;
    }

    .grid {
      display: grid;
      gap: 18px;
    }

    .grid-4 { grid-template-columns: repeat(4, 1fr); }
    .grid-3 { grid-template-columns: repeat(3, 1fr); }
    .grid-2 { grid-template-columns: repeat(2, 1fr); }

    .card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      padding: 20px;
    }

    .stat-card {
      position: relative;
      overflow: hidden;
    }

    .stat-card .stat-icon {
      width: 42px;
      height: 42px;
      border-radius: 12px;
      display: grid;
      place-items: center;
      background: rgba(99, 102, 241, 0.1);
      color: var(--primary);
      margin-bottom: 15px;
      font-size: 20px;
    }

    .stat-card h3 {
      font-size: 28px;
      margin-bottom: 5px;
    }

    .stat-card p {
      color: var(--muted);
      font-size: 14px;
    }

    .card-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
      margin-bottom: 18px;
    }

    .card-header h2,
    .card-header h3 {
      font-size: 18px;
    }

    .muted { color: var(--muted); }

    /* TEMPLATES & ZONES */
    .template-card {
      position: relative;
      margin-bottom: 20px;
    }

    .template-card h3 { margin-bottom: 7px; }

    .template-meta {
      color: var(--muted);
      font-size: 14px;
      margin-bottom: 18px;
    }

    .template-actions {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
    }

    .zone {
      background: var(--card-2);
      border: 1px solid var(--border);
      border-radius: 14px;
      margin-bottom: 16px;
      overflow: hidden;
    }

    .zone-header {
      padding: 15px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: rgba(99, 102, 241, 0.06);
    }

    .zone-title {
      font-weight: 800;
      display: flex;
      gap: 8px;
      align-items: center;
    }

    .exercise-list { padding: 10px 15px 15px; }

    .exercise-row {
      display: grid;
      grid-template-columns: 1.5fr 0.7fr 0.7fr 0.7fr auto;
      gap: 8px;
      align-items: center;
      padding: 10px 0;
      border-bottom: 1px solid var(--border);
    }

    .exercise-row:last-child { border-bottom: 0; }
    .exercise-name { font-weight: 650; }
    .exercise-detail { font-size: 13px; color: var(--muted); }

    /* FORMS */
    .form-group { margin-bottom: 15px; }
    .form-group label {
      display: block;
      font-size: 13px;
      font-weight: 700;
      margin-bottom: 7px;
      color: var(--muted);
    }

    input, select, textarea {
      width: 100%;
      padding: 11px 12px;
      border: 1px solid var(--border);
      background: var(--card);
      color: var(--text);
      border-radius: 10px;
      outline: none;
    }

    input:focus, select:focus, textarea:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.1);
    }

    textarea { resize: vertical; min-height: 100px; }

    .form-row {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 12px;
    }

    .form-row-3 {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 12px;
    }

    /* MODAL */
    .modal-overlay {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0, 0, 0, 0.6);
      z-index: 1000;
      padding: 20px;
      overflow-y: auto;
    }

    .modal-overlay.show {
      display: flex;
      justify-content: center;
      align-items: flex-start;
    }

    .modal {
      background: var(--card);
      width: 100%;
      max-width: 700px;
      margin: 30px auto;
      border-radius: 20px;
      padding: 24px;
      box-shadow: 0 25px 80px rgba(0, 0, 0, 0.3);
    }

    .modal-large { max-width: 1000px; }

    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 22px;
    }

    .modal-close {
      border: 0;
      background: transparent;
      color: var(--muted);
      font-size: 25px;
    }

    .modal-footer {
      display: flex;
      justify-content: flex-end;
      gap: 10px;
      margin-top: 20px;
    }

    /* WORKOUT BUILDER */
    .builder-zone {
      border: 1px solid var(--border);
      border-radius: 14px;
      margin-bottom: 15px;
      overflow: hidden;
    }

    .builder-zone-header {
      padding: 12px;
      background: var(--card-2);
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .builder-exercises { padding: 12px; }

    .builder-exercise {
      display: grid;
      grid-template-columns: 1fr 80px 80px 80px auto;
      gap: 7px;
      margin-bottom: 8px;
      align-items: center;
    }

    .builder-exercise:last-child { margin-bottom: 0; }

    .add-zone-area {
      border: 2px dashed var(--border);
      border-radius: 12px;
      padding: 20px;
      text-align: center;
      margin-top: 15px;
    }

    /* WEIGHT TRACKER & UNITS */
    .weight-input { display: flex; gap: 8px; }
    .weight-input input { flex: 1; }

    .unit-toggle {
      display: flex;
      background: var(--card-2);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 3px;
    }

    .unit-toggle button {
      border: 0;
      padding: 7px 12px;
      border-radius: 7px;
      background: transparent;
      color: var(--muted);
    }

    .unit-toggle button.active {
      background: var(--primary);
      color: white;
    }

    .weight-history {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .weight-entry {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 13px;
      border-radius: 10px;
      background: var(--card-2);
    }

    /* SUGGESTIONS */
    .suggestion {
      border: 1px solid var(--border);
      background: var(--card-2);
      border-radius: 12px;
      padding: 13px;
      margin-bottom: 8px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
    }

    .suggestion-name { font-weight: 700; }
    .suggestion-zone { font-size: 12px; color: var(--muted); }

    /* EMPTY STATES & TOAST */
    .empty {
      text-align: center;
      padding: 40px 20px;
      color: var(--muted);
    }

    .empty-icon {
      font-size: 40px;
      margin-bottom: 10px;
    }

    .toast {
      position: fixed;
      right: 20px;
      bottom: 20px;
      background: #111827;
      color: white;
      padding: 13px 18px;
      border-radius: 10px;
      opacity: 0;
      transform: translateY(20px);
      transition: 0.25s;
      z-index: 3000;
      pointer-events: none;
    }

    .toast.show {
      opacity: 1;
      transform: translateY(0);
    }

    /* MOBILE HEADER */
    .mobile-header { display: none; }

    @media (max-width: 1100px) {
      .grid-4, .grid-3 { grid-template-columns: repeat(2, 1fr); }
    }

    @media (max-width: 800px) {
      .sidebar { display: none; }
      .main { margin-left: 0; width: 100%; padding: 16px; padding-top: 75px; }

      .mobile-header {
        display: flex;
        position: fixed;
        top: 0; left: 0; right: 0;
        height: 60px;
        background: var(--card);
        border-bottom: 1px solid var(--border);
        z-index: 500;
        align-items: center;
        justify-content: space-between;
        padding: 10px 15px;
      }

      .mobile-menu { display: flex; gap: 6px; }
      .mobile-menu button {
        border: 0; background: transparent;
        color: var(--muted); padding: 7px; font-size: 18px;
      }

      .topbar h1 { font-size: 24px; }
      .grid-4, .grid-3, .grid-2, .form-row, .form-row-3 { grid-template-columns: 1fr; }
      .exercise-row, .builder-exercise { grid-template-columns: 1fr 1fr; }
      .top-actions { flex-wrap: wrap; }
    }

    @media (max-width: 500px) {
      .topbar { flex-direction: column; align-items: flex-start; }
      .top-actions { width: 100%; }
      .top-actions .btn { flex: 1; }
    }
  </style>
</head>

<body>

<div class="app">

  <!-- MOBILE HEADER -->
  <header class="mobile-header">
    <div class="logo" style="padding:0;">
      <div class="logo-icon">🏋️</div>
      <span>GymTrack</span>
    </div>

    <div class="mobile-menu">
      <button onclick="showSection('dashboard')" title="Dashboard">🏠</button>
      <button onclick="showSection('templates')" title="Templates">📋</button>
      <button onclick="showSection('weight')" title="Weight">⚖️</button>
      <button onclick="toggleTheme()" title="Theme">🌓</button>
    </div>
  </header>

  <!-- SIDEBAR -->
  <aside class="sidebar">
    <div class="logo">
      <div class="logo-icon">🏋️</div>
      <span>GymTrack</span>
    </div>

    <nav class="nav">
      <button class="active" onclick="showSection('dashboard')" data-section="dashboard">
        🏠 Dashboard
      </button>

      <button onclick="showSection('templates')" data-section="templates">
        📋 Workout Templates
      </button>

      <button onclick="showSection('weight')" data-section="weight">
        ⚖️ Weight Tracker
      </button>

      <button onclick="showSection('suggestions')" data-section="suggestions">
        💡 Exercises
      </button>
    </nav>

    <div class="sidebar-bottom">
      <button class="btn" onclick="toggleTheme()">
        🌓 Toggle Theme
      </button>

      <button class="btn" onclick="exportData()">
        📤 Export Data
      </button>

      <button class="btn" onclick="document.getElementById('importFile').click()">
        📥 Import Data
      </button>

      <input
        id="importFile"
        type="file"
        accept=".json"
        style="display:none"
        onchange="importData(event)"
      />
    </div>
  </aside>

  <!-- MAIN -->
  <main class="main">

    <!-- DASHBOARD -->
    <section id="dashboard" class="section active">
      <div class="topbar">
        <div>
          <h1>Dashboard</h1>
          <p>Your training overview</p>
        </div>

        <div class="top-actions">
          <button class="btn btn-primary" onclick="openTemplateModal()">
            + New Template
          </button>

          <button class="btn" onclick="showSection('weight')">
            + Log Weight
          </button>
        </div>
      </div>

      <div class="grid grid-4">
        <div class="card stat-card">
          <div class="stat-icon">📋</div>
          <h3 id="statTemplates">0</h3>
          <p>Workout Templates</p>
        </div>

        <div class="card stat-card">
          <div class="stat-icon">💪</div>
          <h3 id="statExercises">0</h3>
          <p>Total Exercises</p>
        </div>

        <div class="card stat-card">
          <div class="stat-icon">⚖️</div>
          <h3 id="statWeight">--</h3>
          <p>Current Weight</p>
        </div>

        <div class="card stat-card">
          <div class="stat-icon">🔥</div>
          <h3 id="statWorkouts">0</h3>
          <p>Completed Workouts</p>
        </div>
      </div>

      <div style="height:18px;"></div>

      <div class="grid grid-2">
        <div class="card">
          <div class="card-header">
            <h2>Recent Weight</h2>
            <button class="btn btn-small" onclick="showSection('weight')">
              View All
            </button>
          </div>
          <div id="dashboardWeight"></div>
        </div>

        <div class="card">
          <div class="card-header">
            <h2>Your Templates</h2>
            <button class="btn btn-small" onclick="showSection('templates')">
              View All
            </button>
          </div>
          <div id="dashboardTemplates"></div>
        </div>
      </div>
    </section>

    <!-- TEMPLATES -->
    <section id="templates" class="section">
      <div class="topbar">
        <div>
          <h1>Workout Templates</h1>
          <p>Create and organize your training plans.</p>
        </div>

        <button class="btn btn-primary" onclick="openTemplateModal()">
          + New Template
        </button>
      </div>

      <div id="templatesContainer"></div>
    </section>

    <!-- WEIGHT -->
    <section id="weight" class="section">
      <div class="topbar">
        <div>
          <h1>Weight Tracker</h1>
          <p>Track your body weight over time.</p>
        </div>
      </div>

      <div class="grid grid-2">
        <div class="card">
          <div class="card-header">
            <h2>Log Weight</h2>
          </div>

          <div class="form-group">
            <label>Date</label>
            <input type="date" id="weightDate" />
          </div>

          <div class="form-group">
            <label>Weight</label>
            <div class="weight-input">
              <input type="number" step="0.1" id="weightValue" placeholder="e.g. 80" />
              <div class="unit-toggle">
                <button id="kgButton" class="active" onclick="setWeightUnit('kg')">KG</button>
                <button id="lbButton" onclick="setWeightUnit('lb')">LB</button>
              </div>
            </div>
          </div>

          <div class="form-group">
            <label>Notes</label>
            <textarea id="weightNotes" placeholder="Optional notes..."></textarea>
          </div>

          <button class="btn btn-primary" onclick="addWeight()">
            Save Weight
          </button>
        </div>

        <div class="card">
          <div class="card-header">
            <h2>Weight Trend</h2>
          </div>
          <canvas id="weightChart" style="width:100%; height:180px; margin-bottom:15px;"></canvas>
          
          <div class="card-header">
            <h2>History Log</h2>
          </div>
          <div id="weightHistory" class="weight-history"></div>
        </div>
      </div>
    </section>

    <!-- EXERCISE SUGGESTIONS -->
    <section id="suggestions" class="section">
      <div class="topbar">
        <div>
          <h1>Exercise Library</h1>
          <p>Exercise ideas organized by training zone.</p>
        </div>
      </div>

      <div id="suggestionsContainer"></div>
    </section>

  </main>
</div>

<!-- TEMPLATE MODAL -->
<div id="templateModal" class="modal-overlay">
  <div class="modal modal-large">
    <div class="modal-header">
      <h2 id="templateModalTitle">Create Workout Template</h2>
      <button class="modal-close" onclick="closeModal('templateModal')">×</button>
    </div>

    <input type="hidden" id="editingTemplateId" />

    <div class="form-group">
      <label>Template Name</label>
      <input id="templateName" placeholder="e.g. Push Day" />
    </div>

    <div class="form-group">
      <label>Description</label>
      <input id="templateDescription" placeholder="e.g. Chest, shoulders and triceps" />
    </div>

    <div class="card-header">
      <h3>Training Zones</h3>
    </div>

    <div id="builderZones"></div>

    <div class="add-zone-area">
      <div class="form-row">
        <input id="newZoneName" placeholder="Zone / muscle group e.g. Chest" />
        <button class="btn btn-primary" onclick="addZoneToBuilder()">
          + Add Zone
        </button>
      </div>
    </div>

    <div class="modal-footer">
      <button class="btn" onclick="closeModal('templateModal')">Cancel</button>
      <button class="btn btn-primary" onclick="saveTemplate()">Save Template</button>
    </div>
  </div>
</div>

<!-- WORKOUT EXECUTION MODAL -->
<div id="workoutModal" class="modal-overlay">
  <div class="modal modal-large">
    <div class="modal-header">
      <h2 id="workoutTitle">Workout Session</h2>
      <button class="modal-close" onclick="closeModal('workoutModal')">×</button>
    </div>

    <div id="workoutContent"></div>

    <div class="modal-footer">
      <button class="btn" onclick="closeModal('workoutModal')">Close</button>
      <button class="btn btn-success" onclick="completeWorkout()">✓ Complete Workout</button>
    </div>
  </div>
</div>

<!-- TOAST -->
<div id="toast" class="toast"></div>

<script>
/* DATA & INITIALIZATION */
const STORAGE_KEY = "gymtrack_data";

function generateId() {
  return Date.now().toString(36) + Math.random().toString(36).substring(2, 9);
}

const defaultData = {
  templates: [
    {
      id: generateId(),
      name: "Push Day",
      description: "Chest, shoulders and triceps",
      zones: [
        {
          id: generateId(),
          name: "Chest",
          exercises: [
            { id: generateId(), name: "Barbell Bench Press", sets: 4, reps: 8, weight: 60 },
            { id: generateId(), name: "Incline Dumbbell Press", sets: 3, reps: 10, weight: 22 }
          ]
        },
        {
          id: generateId(),
          name: "Shoulders",
          exercises: [
            { id: generateId(), name: "Overhead Press", sets: 3, reps: 8, weight: 40 },
            { id: generateId(), name: "Lateral Raises", sets: 3, reps: 12, weight: 10 }
          ]
        }
      ]
    },
    {
      id: generateId(),
      name: "Pull Day",
      description: "Back and biceps",
      zones: [
        {
          id: generateId(),
          name: "Back",
          exercises: [
            { id: generateId(), name: "Lat Pulldown", sets: 4, reps: 10, weight: 50 },
            { id: generateId(), name: "Barbell Row", sets: 3, reps: 8, weight: 50 }
          ]
        },
        {
          id: generateId(),
          name: "Biceps",
          exercises: [
            { id: generateId(), name: "Barbell Curl", sets: 3, reps: 10, weight: 25 }
          ]
        }
      ]
    }
  ],
  weights: [],
  workoutHistory: [],
  theme: "light"
};

const exerciseLibrary = {
  "Chest": ["Barbell Bench Press", "Incline Dumbbell Press", "Chest Flyes", "Dips", "Push-ups"],
  "Back": ["Lat Pulldown", "Seated Cable Row", "Barbell Row", "Pull-ups", "Deadlift"],
  "Shoulders": ["Overhead Press", "Lateral Raises", "Front Raises", "Face Pulls"],
  "Legs": ["Barbell Squat", "Leg Press", "Romanian Deadlift", "Leg Curl", "Calf Raises"],
  "Arms": ["Barbell Curl", "Hammer Curl", "Tricep Pushdown", "Skull Crushers"]
};

let data = loadData();
let currentWeightUnit = "kg";
let currentWorkoutTemplate = null;
let builderState = { name: "", description: "", zones: [] };

document.addEventListener("DOMContentLoaded", () => {
  applyTheme();
  document.getElementById("weightDate").value = new Date().toISOString().split("T")[0];
  renderAll();
});

/* STORAGE & HELPERS */
function loadData() {
  const saved = localStorage.getItem(STORAGE_KEY);
  if (!saved) return defaultData;
  try { return { ...defaultData, ...JSON.parse(saved) }; }
  catch (e) { return defaultData; }
}

function saveData() {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
}

function escapeHtml(str) {
  return String(str).replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;').replace(/"/g, '&quot;');
}

function formatDate(dateStr) {
  return new Date(dateStr).toLocaleDateString(undefined, { month: 'short', day: 'numeric', year: 'numeric' });
}

function showToast(msg) {
  const toast = document.getElementById("toast");
  toast.textContent = msg;
  toast.classList.add("show");
  setTimeout(() => toast.classList.remove("show"), 3000);
}

/* NAVIGATION & THEME */
function showSection(sectionId) {
  document.querySelectorAll(".section").forEach(s => s.classList.remove("active"));
  document.getElementById(sectionId).classList.add("active");

  document.querySelectorAll(".nav button").forEach(b => {
    b.classList.toggle("active", b.dataset.section === sectionId);
  });
  window.scrollTo({ top: 0, behavior: "smooth" });
}

function toggleTheme() {
  data.theme = data.theme === "dark" ? "light" : "dark";
  saveData();
  applyTheme();
}

function applyTheme() {
  document.body.classList.toggle("dark", data.theme === "dark");
  renderWeightChart();
}

/* MODALS */
function openModal(modalId) {
  document.getElementById(modalId).classList.add("show");
}

function closeModal(modalId) {
  document.getElementById(modalId).classList.remove("show");
}

/* RENDERING */
function renderAll() {
  renderDashboard();
  renderTemplates();
  renderWeightHistory();
  renderSuggestions();
}

function renderDashboard() {
  const templateCount = data.templates.length;
  const exerciseCount = data.templates.reduce((acc, t) => 
    acc + t.zones.reduce((zAcc, z) => zAcc + z.exercises.length, 0), 0);

  document.getElementById("statTemplates").textContent = templateCount;
  document.getElementById("statExercises").textContent = exerciseCount;
  document.getElementById("statWorkouts").textContent = data.workoutHistory.length;

  const latestWeight = data.weights.length ? data.weights[data.weights.length - 1] : null;
  document.getElementById("statWeight").textContent = latestWeight ? `${latestWeight.kg.toFixed(1)} KG` : "--";

  renderDashboardWeight();
  renderDashboardTemplates();
}

function renderDashboardWeight() {
  const container = document.getElementById("dashboardWeight");
  if (!data.weights.length) {
    container.innerHTML = `<div class="empty"><div class="empty-icon">⚖️</div><p>No weight entries yet.</p></div>`;
    return;
  }
  const recent = [...data.weights].reverse().slice(0, 4);
  container.innerHTML = recent.map(w => `
    <div class="weight-entry">
      <div>
        <strong>${w.kg.toFixed(1)} KG</strong>
        <div class="exercise-detail">${w.lb.toFixed(1)} LB</div>
      </div>
      <div class="muted">${formatDate(w.date)}</div>
    </div>
  `).join("");
}

function renderDashboardTemplates() {
  const container = document.getElementById("dashboardTemplates");
  if (!data.templates.length) {
    container.innerHTML = `<div class="empty"><div class="empty-icon">📋</div><p>No templates yet.</p></div>`;
    return;
  }
  container.innerHTML = data.templates.slice(0, 4).map(t => {
    const exCount = t.zones.reduce((acc, z) => acc + z.exercises.length, 0);
    return `
      <div class="weight-entry">
        <div>
          <strong>${escapeHtml(t.name)}</strong>
          <div class="exercise-detail">${t.zones.length} zones · ${exCount} exercises</div>
        </div>
        <button class="btn btn-small" onclick="startWorkout('${t.id}')">Start</button>
      </div>
    `;
  }).join("");
}

function renderTemplates() {
  const container = document.getElementById("templatesContainer");
  if (!data.templates.length) {
    container.innerHTML = `<div class="card empty"><div class="empty-icon">🏋️</div><p>No templates added yet.</p></div>`;
    return;
  }

  container.innerHTML = data.templates.map(t => `
    <div class="card template-card">
      <div class="card-header">
        <div>
          <h3>${escapeHtml(t.name)}</h3>
          <div class="template-meta">${escapeHtml(t.description || "No description")}</div>
        </div>
        <div class="template-actions">
          <button class="btn btn-primary btn-small" onclick="startWorkout('${t.id}')">▶ Start Workout</button>
          <button class="btn btn-small" onclick="openTemplateModal('${t.id}')">✏️ Edit</button>
          <button class="btn btn-danger btn-small" onclick="deleteTemplate('${t.id}')">🗑️ Delete</button>
        </div>
      </div>
      ${t.zones.map(z => `
        <div class="zone">
          <div class="zone-header">
            <span class="zone-title">📍 ${escapeHtml(z.name)}</span>
          </div>
          <div class="exercise-list">
            ${z.exercises.map(ex => `
              <div class="exercise-row">
                <span class="exercise-name">${escapeHtml(ex.name)}</span>
                <span class="exercise-detail">${ex.sets} Sets</span>
                <span class="exercise-detail">${ex.reps} Reps</span>
                <span class="exercise-detail">${ex.weight ? ex.weight + ' kg' : 'Bodyweight'}</span>
              </div>
            `).join("")}
          </div>
        </div>
      `).join("")}
    </div>
  `).join("");
}

/* TEMPLATE BUILDER */
function openTemplateModal(templateId = null) {
  if (templateId) {
    const t = data.templates.find(item => item.id === templateId);
    builderState = JSON.parse(JSON.stringify(t));
    document.getElementById("templateModalTitle").textContent = "Edit Workout Template";
    document.getElementById("editingTemplateId").value = templateId;
  } else {
    builderState = { id: generateId(), name: "", description: "", zones: [] };
    document.getElementById("templateModalTitle").textContent = "Create Workout Template";
    document.getElementById("editingTemplateId").value = "";
  }

  document.getElementById("templateName").value = builderState.name;
  document.getElementById("templateDescription").value = builderState.description;
  renderBuilderZones();
  openModal("templateModal");
}

function renderBuilderZones() {
  const container = document.getElementById("builderZones");
  container.innerHTML = builderState.zones.map((zone, zIdx) => `
    <div class="builder-zone">
      <div class="builder-zone-header">
        <strong>${escapeHtml(zone.name)}</strong>
        <button class="btn btn-danger btn-small" onclick="removeBuilderZone(${zIdx})">Remove Zone</button>
      </div>
      <div class="builder-exercises">
        ${zone.exercises.map((ex, eIdx) => `
          <div class="builder-exercise">
            <input type="text" placeholder="Exercise name" value="${escapeHtml(ex.name)}" onchange="updateBuilderExercise(${zIdx},${eIdx}, 'name', this.value)" />
            <input type="number" placeholder="Sets" value="${ex.sets}" onchange="updateBuilderExercise(${zIdx},${eIdx}, 'sets', this.value)" />
            <input type="number" placeholder="Reps" value="${ex.reps}" onchange="updateBuilderExercise(${zIdx},${eIdx}, 'reps', this.value)" />
            <input type="number" placeholder="Kg" value="${ex.weight || ''}" onchange="updateBuilderExercise(${zIdx},${eIdx}, 'weight', this.value)" />
            <button class="btn btn-danger btn-small" onclick="removeBuilderExercise(${zIdx},${eIdx})">×</button>
          </div>
        `).join("")}
        <button class="btn btn-small" style="margin-top:8px;" onclick="addExerciseToBuilderZone(${zIdx})">+ Add Exercise</button>
      </div>
    </div>
  `).join("");
}

function addZoneToBuilder() {
  const nameInput = document.getElementById("newZoneName");
  const name = nameInput.value.trim();
  if (!name) return;
  builderState.zones.push({ id: generateId(), name, exercises: [] });
  nameInput.value = "";
  renderBuilderZones();
}

function removeBuilderZone(zIdx) {
  builderState.zones.splice(zIdx, 1);
  renderBuilderZones();
}

function addExerciseToBuilderZone(zIdx) {
  builderState.zones[zIdx].exercises.push({ id: generateId(), name: "", sets: 3, reps: 10, weight: 0 });
  renderBuilderZones();
}

function updateBuilderExercise(zIdx, eIdx, field, val) {
  builderState.zones[zIdx].exercises[eIdx][field] = field === 'name' ? val : Number(val);
}

function removeBuilderExercise(zIdx, eIdx) {
  builderState.zones[zIdx].exercises.splice(eIdx, 1);
  renderBuilderZones();
}

function saveTemplate() {
  builderState.name = document.getElementById("templateName").value.trim() || "Untitled Workout";
  builderState.description = document.getElementById("templateDescription").value.trim();

  if (!builderState.zones.length) {
    alert("Please add at least one zone and exercise.");
    return;
  }

  const editId = document.getElementById("editingTemplateId").value;
  if (editId) {
    const idx = data.templates.findIndex(t => t.id === editId);
    if (idx !== -1) data.templates[idx] = builderState;
  } else {
    data.templates.push(builderState);
  }

  saveData();
  renderAll();
  closeModal("templateModal");
  showToast("Template saved successfully!");
}

function deleteTemplate(id) {
  if (confirm("Delete this workout template?")) {
    data.templates = data.templates.filter(t => t.id !== id);
    saveData();
    renderAll();
    showToast("Template deleted.");
  }
}

/* WORKOUT EXECUTION */
function startWorkout(templateId) {
  const template = data.templates.find(t => t.id === templateId);
  if (!template) return;

  currentWorkoutTemplate = JSON.parse(JSON.stringify(template));
  document.getElementById("workoutTitle").textContent = currentWorkoutTemplate.name;

  const container = document.getElementById("workoutContent");
  container.innerHTML = currentWorkoutTemplate.zones.map(z => `
    <div class="zone">
      <div class="zone-header">
        <span class="zone-title">📍 ${escapeHtml(z.name)}</span>
      </div>
      <div class="exercise-list">
        ${z.exercises.map(ex => `
          <div style="margin-bottom: 12px;">
            <strong>${escapeHtml(ex.name)}</strong>
            <div class="form-row-3" style="margin-top:6px;">
              <div>
                <label style="font-size:11px;">Target Sets</label>
                <input type="number" value="${ex.sets}" disabled />
              </div>
              <div>
                <label style="font-size:11px;">Reps Performed</label>
                <input type="number" value="${ex.reps}" />
              </div>
              <div>
                <label style="font-size:11px;">Weight (kg)</label>
                <input type="number" value="${ex.weight}" />
              </div>
            </div>
          </div>
        `).join("")}
      </div>
    </div>
  `).join("");

  openModal("workoutModal");
}

function completeWorkout() {
  data.workoutHistory.push({
    id: generateId(),
    templateId: currentWorkoutTemplate.id,
    name: currentWorkoutTemplate.name,
    date: new Date().toISOString()
  });

  saveData();
  renderDashboard();
  closeModal("workoutModal");
  showToast("Workout logged! Great job! 🎉");
}

/* WEIGHT TRACKER */
function setWeightUnit(unit) {
  currentWeightUnit = unit;
  document.getElementById("kgButton").classList.toggle("active", unit === 'kg');
  document.getElementById("lbButton").classList.toggle("active", unit === 'lb');
}

function addWeight() {
  const val = parseFloat(document.getElementById("weightValue").value);
  const date = document.getElementById("weightDate").value;
  const notes = document.getElementById("weightNotes").value.trim();

  if (isNaN(val) || !date) {
    alert("Please enter a valid weight and date.");
    return;
  }

  const kg = currentWeightUnit === "kg" ? val : val / 2.20462;
  const lb = currentWeightUnit === "lb" ? val : val * 2.20462;

  data.weights.push({ id: generateId(), date, kg, lb, notes });
  data.weights.sort((a, b) => new Date(a.date) - new Date(b.date));

  saveData();
  renderAll();
  document.getElementById("weightValue").value = "";
  document.getElementById("weightNotes").value = "";
  showToast("Weight recorded!");
}

function deleteWeight(id) {
  data.weights = data.weights.filter(w => w.id !== id);
  saveData();
  renderAll();
  showToast("Entry removed.");
}

function renderWeightHistory() {
  const container = document.getElementById("weightHistory");
  if (!data.weights.length) {
    container.innerHTML = `<div class="empty"><p>No weight logs available.</p></div>`;
    return;
  }

  container.innerHTML = [...data.weights].reverse().map(w => `
    <div class="weight-entry">
      <div>
        <strong>${w.kg.toFixed(1)} KG / ${w.lb.toFixed(1)} LB</strong>
        <div class="exercise-detail">${formatDate(w.date)} ${w.notes ? '• ' + escapeHtml(w.notes) : ''}</div>
      </div>
      <button class="btn btn-danger btn-small" onclick="deleteWeight('${w.id}')">🗑️</button>
    </div>
  `).join("");

  renderWeightChart();
}

function renderWeightChart() {
  const canvas = document.getElementById("weightChart");
  if (!canvas) return;
  const ctx = canvas.getContext("2d");
  
  canvas.width = canvas.parentElement.clientWidth - 40;
  canvas.height = 180;

  ctx.clearRect(0, 0, canvas.width, canvas.height);

  if (data.weights.length < 2) {
    ctx.fillStyle = data.theme === 'dark' ? '#94a3b8' : '#6b7280';
    ctx.font = '13px Inter';
    ctx.fillText('Log at least 2 entries to display weight progress chart.', 10, 90);
    return;
  }

  const padding = 30;
  const weights = data.weights.map(w => w.kg);
  const minW = Math.min(...weights) - 2;
  const maxW = Math.max(...weights) + 2;

  ctx.beginPath();
  ctx.strokeStyle = '#6366f1';
  ctx.lineWidth = 3;

  weights.forEach((w, i) => {
    const x = padding + (i / (weights.length - 1)) * (canvas.width - padding * 2);
    const y = canvas.height - padding - ((w - minW) / (maxW - minW)) * (canvas.height - padding * 2);

    if (i === 0) ctx.moveTo(x, y);
    else ctx.lineTo(x, y);
  });

  ctx.stroke();
}

/* EXERCISE SUGGESTIONS */
function renderSuggestions() {
  const container = document.getElementById("suggestionsContainer");
  container.innerHTML = Object.entries(exerciseLibrary).map(([zone, items]) => `
    <div class="card" style="margin-bottom: 16px;">
      <div class="card-header">
        <h2>${zone}</h2>
      </div>
      ${items.map(ex => `
        <div class="suggestion">
          <div>
            <div class="suggestion-name">${ex}</div>
            <div class="suggestion-zone">Primary Target: ${zone}</div>
          </div>
        </div>
      `).join("")}
    </div>
  `).join("");
}

/* EXPORT / IMPORT */
function exportData() {
  const blob = new Blob([JSON.stringify(data, null, 2)], { type: "application/json" });
  const url = URL.createObjectURL(blob);
  const a = document.createElement("a");
  a.href = url;
  a.download = `gymtrack_backup_${new Date().toISOString().split('T')[0]}.json`;
  a.click();
  URL.revokeObjectURL(url);
}

function importData(e) {
  const file = e.target.files[0];
  if (!file) return;

  const reader = new FileReader();
  reader.onload = (event) => {
    try {
      const imported = JSON.parse(event.target.result);
      if (imported.templates && imported.weights) {
        data = imported;
        saveData();
        renderAll();
        showToast("Data imported successfully!");
      } else {
        alert("Invalid file structure.");
      }
    } catch (err) {
      alert("Error parsing backup JSON file.");
    }
  };
  reader.readAsText(file);
}
</script>

</body>
</html>
