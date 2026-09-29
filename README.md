#GymTrack
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

    /* =========================
       SIDEBAR
    ========================= */

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

    /* =========================
       MAIN
    ========================= */

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

    /* =========================
       BUTTONS
    ========================= */

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

    /* =========================
       SECTIONS
    ========================= */

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

    .grid-4 {
      grid-template-columns: repeat(4, 1fr);
    }

    .grid-3 {
      grid-template-columns: repeat(3, 1fr);
    }

    .grid-2 {
      grid-template-columns: repeat(2, 1fr);
    }

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

    .muted {
      color: var(--muted);
    }

    /* =========================
       TEMPLATES
    ========================= */

    .template-card {
      position: relative;
    }

    .template-card h3 {
      margin-bottom: 7px;
    }

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

    .exercise-list {
      padding: 10px 15px 15px;
    }

    .exercise-row {
      display: grid;
      grid-template-columns: 1.5fr 0.7fr 0.7fr 0.7fr auto;
      gap: 8px;
      align-items: center;
      padding: 10px 0;
      border-bottom: 1px solid var(--border);
    }

    .exercise-row:last-child {
      border-bottom: 0;
    }

    .exercise-name {
      font-weight: 650;
    }

    .exercise-detail {
      font-size: 13px;
      color: var(--muted);
    }

    /* =========================
       FORMS
    ========================= */

    .form-group {
      margin-bottom: 15px;
    }

    .form-group label {
      display: block;
      font-size: 13px;
      font-weight: 700;
      margin-bottom: 7px;
      color: var(--muted);
    }

    input,
    select,
    textarea {
      width: 100%;
      padding: 11px 12px;
      border: 1px solid var(--border);
      background: var(--card);
      color: var(--text);
      border-radius: 10px;
      outline: none;
    }

    input:focus,
    select:focus,
    textarea:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.1);
    }

    textarea {
      resize: vertical;
      min-height: 100px;
    }

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

    /* =========================
       MODAL
    ========================= */

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

    .modal-large {
      max-width: 1000px;
    }

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

    /* =========================
       WORKOUT BUILDER
    ========================= */

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

    .builder-exercises {
      padding: 12px;
    }

    .builder-exercise {
      display: grid;
      grid-template-columns: 1fr 80px 80px 80px auto;
      gap: 7px;
      margin-bottom: 8px;
      align-items: center;
    }

    .builder-exercise:last-child {
      margin-bottom: 0;
    }

    .add-zone-area {
      border: 2px dashed var(--border);
      border-radius: 12px;
      padding: 20px;
      text-align: center;
      margin-top: 15px;
    }

    /* =========================
       WEIGHT
    ========================= */

    .weight-input {
      display: flex;
      gap: 8px;
    }

    .weight-input input {
      flex: 1;
    }

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

    /* =========================
       SUGGESTIONS
    ========================= */

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

    .suggestion-name {
      font-weight: 700;
    }

    .suggestion-zone {
      font-size: 12px;
      color: var(--muted);
    }

    /* =========================
       EMPTY
    ========================= */

    .empty {
      text-align: center;
      padding: 40px 20px;
      color: var(--muted);
    }

    .empty-icon {
      font-size: 40px;
      margin-bottom: 10px;
    }

    /* =========================
       TOAST
    ========================= */

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

    /* =========================
       MOBILE
    ========================= */

    .mobile-header {
      display: none;
    }

    @media (max-width: 1100px) {
      .grid-4 {
        grid-template-columns: repeat(2, 1fr);
      }

      .grid-3 {
        grid-template-columns: repeat(2, 1fr);
      }
    }

    @media (max-width: 800px) {
      .sidebar {
        display: none;
      }

      .main {
        margin-left: 0;
        width: 100%;
        padding: 16px;
        padding-top: 75px;
      }

      .mobile-header {
        display: flex;
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        height: 60px;
        background: var(--card);
        border-bottom: 1px solid var(--border);
        z-index: 500;
        align-items: center;
        justify-content: space-between;
        padding: 10px 15px;
      }

      .mobile-menu {
        display: flex;
        gap: 6px;
      }

      .mobile-menu button {
        border: 0;
        background: transparent;
        color: var(--muted);
        padding: 7px;
        font-size: 18px;
      }

      .topbar h1 {
        font-size: 24px;
      }

      .grid-4,
      .grid-3,
      .grid-2 {
        grid-template-columns: 1fr;
      }

      .form-row,
      .form-row-3 {
        grid-template-columns: 1fr;
      }

      .exercise-row {
        grid-template-columns: 1fr 1fr;
      }

      .builder-exercise {
        grid-template-columns: 1fr 1fr;
      }

      .top-actions {
        flex-wrap: wrap;
      }
    }

    @media (max-width: 500px) {
      .topbar {
        flex-direction: column;
        align-items: flex-start;
      }

      .top-actions {
        width: 100%;
      }

      .top-actions .btn {
        flex: 1;
      }
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
              <input
                type="number"
                step="0.1"
                id="weightValue"
                placeholder="e.g. 80"
              />

              <div class="unit-toggle">
                <button
                  id="kgButton"
                  class="active"
                  onclick="setWeightUnit('kg')"
                >
                  KG
                </button>

                <button
                  id="lbButton"
                  onclick="setWeightUnit('lb')"
                >
                  LB
                </button>
              </div>
            </div>
          </div>

          <div class="form-group">
            <label>Notes</label>
            <textarea
              id="weightNotes"
              placeholder="Optional notes..."
            ></textarea>
          </div>

          <button class="btn btn-primary" onclick="addWeight()">
            Save Weight
          </button>

        </div>


        <div class="card">

          <div class="card-header">
            <h2>Weight History</h2>
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

      <button
        class="modal-close"
        onclick="closeModal('templateModal')"
      >
        ×
      </button>
    </div>

    <input type="hidden" id="editingTemplateId" />

    <div class="form-group">
      <label>Template Name</label>
      <input
        id="templateName"
        placeholder="e.g. Push Day"
      />
    </div>

    <div class="form-group">
      <label>Description</label>
      <input
        id="templateDescription"
        placeholder="e.g. Chest, shoulders and triceps"
      />
    </div>

    <div class="card-header">
      <h3>Training Zones</h3>
    </div>

    <div id="builderZones"></div>

    <div class="add-zone-area">

      <div class="form-row">

        <input
          id="newZoneName"
          placeholder="Zone / muscle group e.g. Chest"
        />

        <button
          class="btn btn-primary"
          onclick="addZoneToBuilder()"
        >
          + Add Zone
        </button>

      </div>

    </div>

    <div class="modal-footer">

      <button
        class="btn"
        onclick="closeModal('templateModal')"
      >
        Cancel
      </button>

      <button
        class="btn btn-primary"
        onclick="saveTemplate()"
      >
        Save Template
      </button>

    </div>

  </div>

</div>


<!-- WORKOUT MODAL -->

<div id="workoutModal" class="modal-overlay">

  <div class="modal modal-large">

    <div class="modal-header">
      <h2 id="workoutTitle">Workout</h2>

      <button
        class="modal-close"
        onclick="closeModal('workoutModal')"
      >
        ×
      </button>
    </div>

    <div id="workoutContent"></div>

    <div class="modal-footer">

      <button
        class="btn"
        onclick="closeModal('workoutModal')"
      >
        Close
      </button>

      <button
        class="btn btn-success"
        onclick="completeWorkout()"
      >
        ✓ Complete Workout
      </button>

    </div>

  </div>

</div>


<!-- TOAST -->

<div id="toast" class="toast"></div>


<script>
/* =========================================================
   DATA
========================================================= */

const STORAGE_KEY = "gymtrack_data";

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
            {
              id: generateId(),
              name: "Barbell Bench Press",
              sets: 4,
              reps: 8,
              weight: 0
            },
            {
              id: generateId(),
              name: "Incline Dumbbell Press",
              sets: 3,
              reps: 10,
              weight: 0
            }
          ]
        },
        {
          id: generateId(),
          name: "Shoulders",
          exercises: [
            {
              id: generateId(),
              name: "Overhead Press",
              sets: 3,
              reps: 8,
              weight: 0
            },
            {
              id: generateId(),
              name: "Lateral Raises",
              sets: 3,
              reps: 12,
              weight: 0
            }
          ]
        },
        {
          id: generateId(),
          name: "Triceps",
          exercises: [
            {
              id: generateId(),
              name: "Tricep Pushdown",
              sets: 3,
              reps: 12,
              weight: 0
            }
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
            {
              id: generateId(),
              name: "Lat Pulldown",
              sets: 4,
              reps: 10,
              weight: 0
            },
            {
              id: generateId(),
              name: "Seated Cable Row",
              sets: 3,
              reps: 10,
              weight: 0
            },
            {
              id: generateId(),
              name: "Barbell Row",
              sets: 3,
              reps: 8,
              weight: 0
            }
          ]
        },

        {
          id: generateId(),
          name: "Biceps",
          exercises: [
            {
              id: generateId(),
              name: "Barbell Curl",
              sets: 3,
              reps: 10,
              weight: 0
            },
            {
              id: generateId(),
              name: "Hammer Curl",
              sets: 3,
              reps: 12,
              weight: 0
            }
          ]
        }
      ]
    },

    {
      id: generateId(),
      name: "Leg Day",
      description: "Quads, hamstrings, glutes and calves",
      zones: [
        {
          id: generateId(),
          name: "Quads",
          exercises: [
            {
              id: generateId(),
              name: "Barbell Squat",
              sets: 4,
              reps: 8,
              weight: 0
            },
            {
              id: generateId(),
              name: "Leg Press",
              sets: 3,
              reps: 10,
              weight: 0
            }
          ]
        },

        {
          id: generateId(),
          name: "Hamstrings",
          exercises: [
            {
              id: generateId(),
              name: "Romanian Deadlift",
              sets: 3,
              reps: 10,
              weight: 0
            },
            {
              id: generateId(),
              name: "Leg Curl",
              sets: 3,
              reps: 12,
              weight: 0
            }
          ]
        },

        {
          id: generateId(),
          name: "Calves",
          exercises: [
            {
              id: generateId(),
              name: "Standing Calf Raise",
              sets: 4,
              reps: 15,
              weight: 0
            }
          ]
        }
      ]
    }
  ],

  weights: [],

  workoutHistory: [],

  theme: "light"
};


/* =========================================================
   STATE
========================================================= */

let data = loadData();

let currentWeightUnit = "kg";

let currentWorkoutTemplate = null;


/* =========================================================
   INITIALIZATION
========================================================= */

document.addEventListener("DOMContentLoaded", () => {

  applyTheme();

  document.getElementById("weightDate").value =
    new Date().toISOString().split("T")[0];

  renderAll();

});


/* =========================================================
   STORAGE
========================================================= */

function loadData() {

  const saved = localStorage.getItem(STORAGE_KEY);

  if (!saved) {
    return defaultData;
  }

  try {

    const parsed = JSON.parse(saved);

    return {
      ...defaultData,
      ...parsed
    };

  } catch (error) {

    console.error("Could not load saved data.", error);

    return defaultData;
  }
}


function saveData() {

  localStorage.setItem(
    STORAGE_KEY,
    JSON.stringify(data)
  );

}


/* =========================================================
   ID
========================================================= */

function generateId() {

  return Date.now().toString(36) +
    Math.random().toString(36).substring(2, 9);

}


/* =========================================================
   NAVIGATION
========================================================= */

function showSection(sectionId) {

  document.querySelectorAll(".section")
    .forEach(section => {
      section.classList.remove("active");
    });

  document
    .getElementById(sectionId)
    .classList.add("active");

  document.querySelectorAll(".nav button")
    .forEach(button => {

      button.classList.remove("active");

      if (button.dataset.section === sectionId) {
        button.classList.add("active");
      }

    });

  window.scrollTo({
    top: 0,
    behavior: "smooth"
  });

}


/* =========================================================
   THEME
========================================================= */

function toggleTheme() {

  data.theme =
    data.theme === "dark"
      ? "light"
      : "dark";

  saveData();

  applyTheme();

}


function applyTheme() {

  document.body.classList.toggle(
    "dark",
    data.theme === "dark"
  );

}


/* =========================================================
   RENDER ALL
========================================================= */

function renderAll() {

  renderDashboard();

  renderTemplates();

  renderWeightHistory();

  renderSuggestions();

}


/* =========================================================
   DASHBOARD
========================================================= */

function renderDashboard() {

  const templateCount =
    data.templates.length;

  const exerciseCount =
    data.templates.reduce(
      (total, template) => {

        return total +
          template.zones.reduce(
            (zoneTotal, zone) =>
              zoneTotal + zone.exercises.length,
            0
          );

      },
      0
    );

  document.getElementById("statTemplates")
    .textContent = templateCount;

  document.getElementById("statExercises")
    .textContent = exerciseCount;

  document.getElementById("statWorkouts")
    .textContent = data.workoutHistory.length;

  const latestWeight =
    data.weights.length
      ? data.weights[data.weights.length - 1]
      : null;

  document.getElementById("statWeight")
    .textContent = latestWeight
      ? `${latestWeight.kg.toFixed(1)} KG`
      : "--";

  renderDashboardWeight();

  renderDashboardTemplates();

}


function renderDashboardWeight() {

  const container =
    document.getElementById("dashboardWeight");

  if (!data.weights.length) {

    container.innerHTML = `
      <div class="empty">
        <div class="empty-icon">⚖️</div>
        <p>No weight entries yet.</p>
      </div>
    `;

    return;
  }

  const recent =
    [...data.weights]
      .reverse()
      .slice(0, 5);

  container.innerHTML =
    recent.map(weight => {

      return `
        <div class="weight-entry">
          <div>
            <strong>${weight.kg.toFixed(1)} KG</strong>
            <div class="exercise-detail">
              ${weight.lb.toFixed(1)} LB
            </div>
          </div>

          <div class="muted">
            ${formatDate(weight.date)}
          </div>
        </div>
      `;

    }).join("");

}


function renderDashboardTemplates() {

  const container =
    document.getElementById("dashboardTemplates");

  if (!data.templates.length) {

    container.innerHTML = `
      <div class="empty">
        <div class="empty-icon">📋</div>
        <p>No templates yet.</p>
      </div>
    `;

    return;
  }

  container.innerHTML =
    data.templates
      .slice(0, 5)
      .map(template => {

        const exerciseCount =
          template.zones.reduce(
            (total, zone) =>
              total + zone.exercises.length,
            0
          );

        return `
          <div class="weight-entry">
            <div>
              <strong>${escapeHtml(template.name)}</strong>

              <div class="exercise-detail">
                ${template.zones.length} zones ·
                ${exerciseCount} exercises
              </div>
            </div>

            <button
              class="btn btn-small"
              onclick="startWorkout('${template.id}')"
            >
              Start
            </button>
          </div>
        `;

      }).join("");

}


/* =========================================================
   TEMPLATE RENDERING
========================================================= */

function renderTemplates() {

  const container =
    document.getElementById("templatesContainer");

  if (!data.templates.length) {

    container.innerHTML = `
      <div class="card empty">
        <div class="empty-icon">🏋️</div>
        <h3>No workout templates</h3>
        <p>Create your first workout plan.</p>

        <br>

        <button
          class="btn btn-primary"
          onclick="openTemplateModal()"
        >
          + Create Template
        </button>
      </div>
    `;

    return;
  }

  container.innerHTML =
    `<div class="grid grid-2">
      ${data.templates.map(template => {

        return renderTemplateCard(template);

      }).join("")}
    </div>`;

}


function renderTemplateCard(template) {

  const exerciseCount =
    template.zones.reduce(
      (total, zone) =>
        total + zone.exercises.length,
      0
    );

  return `
    <div class="card template-card">

      <div class="card-header">

        <div>
          <h3>${escapeHtml(template.name)}</h3>

          <div class="template-meta">
            ${escapeHtml(template.description || "Custom workout")}
          </div>
        </div>

        <div>
          <button
            class="btn btn-small"
            onclick="editTemplate('${template.id}')"
          >
            ✏️
          </button>
        </div>

      </div>

      <div class="template-meta">
        💪 ${template.zones.length} zones
        &nbsp; · &nbsp;
        🏋️ ${exerciseCount} exercises
      </div>

      <div style="margin-bottom:15px;">

        ${template.zones.map(zone => {

          return `
            <span style="
              display:inline-block;
              background:rgba(99,102,241,.1);
              color:var(--primary);
              padding:5px 9px;
              border-radius:20px;
              font-size:12px;
              margin:2px;
            ">
              ${escapeHtml(zone.name)}
            </span>
          `;

        }).join("")}

      </div>

      <div class="template-actions">

        <button
          class="btn btn-primary"
          onclick="startWorkout('${template.id}')"
        >
          ▶ Start Workout
        </button>

        <button
          class="btn"
          onclick="editTemplate('${template.id}')"
        >
          Edit
        </button>

        <button
          class="btn btn-danger"
          onclick="deleteTemplate('${template.id}')"
        >
          Delete
        </button>

      </div>

    </div>
  `;
}


/* =========================================================
   TEMPLATE MODAL
========================================================= */

function openTemplateModal(template = null) {

  document.getElementById("templateModal")
    .classList.add("show");

  document.getElementById("editingTemplateId")
    .value = template ? template.id : "";

  document.getElementById("templateName")
    .value = template ? template.name : "";

  document.getElementById("templateDescription")
    .value = template ? template.description : "";

  document.getElementById("templateModalTitle")
    .textContent = template
      ? "Edit Workout Template"
      : "Create Workout Template";

  const builder =
    document.getElementById("builderZones");

  builder.innerHTML = "";

  if (template) {

    template.zones.forEach(zone => {

      addZoneToBuilder(zone);

    });

  }

}


function editTemplate(id) {

  const template =
    data.templates.find(
      template => template.id === id
    );

  if (!template) return;

  openTemplateModal(template);

}


function closeModal(id) {

  document.getElementById(id)
    .classList.remove("show");

}


/* =========================================================
   BUILDER
========================================================= */

function addZoneToBuilder(existingZone = null) {

  const nameInput =
    document.getElementById("newZoneName");

  const zoneName =
    existingZone
      ? existingZone.name
      : nameInput.value.trim();

  if (!zoneName) {

    showToast("Enter a zone name first.");

    return;
  }

  const zoneId =
    existingZone
      ? existingZone.id
      : generateId();

  const zone = document.createElement("div");

  zone.className = "builder-zone";

  zone.dataset.zoneId = zoneId;

  zone.innerHTML = `

    <div class="builder-zone-header">

      <strong>
        ${escapeHtml(zoneName)}
      </strong>

      <button
        class="btn btn-small btn-danger"
        onclick="this.closest('.builder-zone').remove()"
      >
        Remove Zone
      </button>

    </div>

    <div class="builder-exercises">

      <div class="builder-exercise">

        <strong>Exercise</strong>
        <strong>Sets</strong>
        <strong>Reps</strong>
        <strong>Weight</strong>
        <span></span>

      </div>

    </div>

    <div style="padding:0 12px 12px;">

      <button
        class="btn btn-small"
        onclick="addExerciseToBuilder(this)"
      >
        + Add Exercise
      </button>

    </div>
  `;

  const exerciseContainer =
    zone.querySelector(".builder-exercises");

  if (existingZone) {

    existingZone.exercises.forEach(exercise => {

      addExerciseToBuilder(
        zone.querySelector(".builder-exercises"),
        exercise
      );

    });

  } else {

    addExerciseToBuilder(
      zone.querySelector(".builder-exercises")
    );

  }

  document
    .getElementById("builderZones")
    .appendChild(zone);

  nameInput.value = "";

}


function addExerciseToBuilder(buttonOrContainer, existingExercise = null) {

  let container;

  if (
    buttonOrContainer &&
    buttonOrContainer.classList &&
    buttonOrContainer.classList.contains("builder-exercises")
  ) {

    container = buttonOrContainer;

  } else {

    container =
      buttonOrContainer
        .closest(".builder-zone")
        .querySelector(".builder-exercises");

  }

  const row =
    document.createElement("div");

  row.className =
    "builder-exercise";

  row.dataset.exerciseId =
    existingExercise
      ? existingExercise.id
      : generateId();

  row.innerHTML = `

    <input
      type="text"
      placeholder="Exercise name"
      value="${existingExercise ? escapeAttribute(existingExercise.name) : ""}"
    />

    <input
      type="number"
      min="1"
      value="${existingExercise ? existingExercise.sets : 3}"
      title="Sets"
    />

    <input
      type="number"
      min="1"
      value="${existingExercise ? existingExercise.reps : 10}"
      title="Reps"
    />

    <input
      type="number"
      min="0"
      step="0.5"
      value="${existingExercise ? existingExercise.weight : 0}"
      title="Weight"
    />

    <button
      class="btn btn-small btn-danger"
      onclick="this.parentElement.remove()"
    >
      ×
    </button>
  `;

  container.appendChild(row);

}


/* =========================================================
   SAVE TEMPLATE
========================================================= */

function saveTemplate() {

  const name =
    document.getElementById("templateName")
      .value.trim();

  const description =
    document.getElementById("templateDescription")
      .value.trim();

  if (!name) {

    showToast("Please enter a template name.");

    return;
  }

  const zoneElements =
    document.querySelectorAll(
      "#builderZones .builder-zone"
    );

  const zones = [];

  zoneElements.forEach(zoneElement => {

    const zoneName =
      zoneElement
        .querySelector(".builder-zone-header strong")
        .textContent.trim();

    const exercises = [];

    const exerciseRows =
      zoneElement.querySelectorAll(
        ".builder-exercises .builder-exercise"
      );

    exerciseRows.forEach(row => {

      const inputs =
        row.querySelectorAll("input");

      if (!inputs[0].value.trim()) return;

      exercises.push({

        id:
          row.dataset.exerciseId ||
          generateId(),

        name:
          inputs[0].value.trim(),

        sets:
          Number(inputs[1].value) || 3,

        reps:
          Number(inputs[2].value) || 10,

        weight:
          Number(inputs[3].value) || 0

      });

    });

    zones.push({

      id:
        zoneElement.dataset.zoneId ||
        generateId(),

      name: zoneName,

      exercises

    });

  });

  const editingId =
    document.getElementById("editingTemplateId")
      .value;

  const template = {

    id:
      editingId ||
      generateId(),

    name,

    description,

    zones

  };

  if (editingId) {

    const index =
      data.templates.findIndex(
        template => template.id === editingId
      );

    if (index !== -1) {

      data.templates[index] =
        template;

    }

  } else {

    data.templates.push(template);

  }

  saveData();

  renderAll();

  closeModal("templateModal");

  showToast(
    editingId
      ? "Template updated."
      : "Template created."
  );

}


/* =========================================================
   DELETE TEMPLATE
========================================================= */

function deleteTemplate(id) {

  const template =
    data.templates.find(
      template => template.id === id
    );

  if (!template) return;

  const confirmed =
    confirm(
      `Delete "${template.name}"?`
    );

  if (!confirmed) return;

  data.templates =
    data.templates.filter(
      template => template.id !== id
    );

  saveData();

  renderAll();

  showToast("Template deleted.");

}


/* =========================================================
   WORKOUT
========================================================= */

function startWorkout(id) {

  const template =
    data.templates.find(
      template => template.id === id
    );

  if (!template) return;

  currentWorkoutTemplate =
    JSON.parse(JSON.stringify(template));

  document.getElementById("workoutTitle")
    .textContent =
      `🏋️ ${template.name}`;

  const container =
    document.getElementById("workoutContent");

  container.innerHTML = `

    <p class="muted" style="margin-bottom:20px;">
      ${escapeHtml(template.description || "")}
    </p>

    ${template.zones.map(zone => `

      <div class="zone">

        <div class="zone-header">

          <div class="zone-title">
            💪 ${escapeHtml(zone.name)}
          </div>

        </div>

        <div class="exercise-list">

          ${zone.exercises.map((exercise, index) => `

            <div class="exercise-row">

              <div>
                <div class="exercise-name">
                  ${escapeHtml(exercise.name)}
                </div>

                <div class="exercise-detail">
                  ${exercise.sets} sets ×
                  ${exercise.reps} reps
                </div>
              </div>

              <input
                type="number"
                min="0"
                step="0.5"
                class="workout-weight"
                data-zone="${zone.id}"
                data-exercise="${exercise.id}"
                value="${exercise.weight || ""}"
                placeholder="Weight"
              />

              <input
                type="number"
                min="1"
                class="workout-sets"
                value="${exercise.sets}"
                placeholder="Sets"
              />

              <input
                type="number"
                min="1"
                class="workout-reps"
                value="${exercise.reps}"
                placeholder="Reps"
              />

              <span></span>

            </div>

          `).join("")}

        </div>

      </div>

    `).join("")}

  `;

  document
    .getElementById("workoutModal")
    .classList.add("show");

}


/* =========================================================
   COMPLETE WORKOUT
========================================================= */

function completeWorkout() {

  if (!currentWorkoutTemplate) return;

  const workoutDate =
    new Date().toISOString();

  data.workoutHistory.push({

    id: generateId(),

    templateId:
      currentWorkoutTemplate.id,

    templateName:
      currentWorkoutTemplate.name,

    date:
      workoutDate

  });

  saveData();

  renderAll();

  closeModal("workoutModal");

  showToast("Workout completed! 💪");

  currentWorkoutTemplate = null;

}


/* =========================================================
   WEIGHT
========================================================= */

function setWeightUnit(unit) {

  currentWeightUnit = unit;

  document
    .getElementById("kgButton")
    .classList.toggle(
      "active",
      unit === "kg"
    );

  document
    .getElementById("lbButton")
    .classList.toggle(
      "active",
      unit === "lb"
    );

}


function addWeight() {

  const value =
    Number(
      document.getElementById("weightValue").value
    );

  const date =
    document.getElementById("weightDate").value;

  const notes =
    document.getElementById("weightNotes")
      .value.trim();

  if (!value || value <= 0) {

    showToast("Enter a valid weight.");

    return;
  }

  if (!date) {

    showToast("Select a date.");

    return;
  }

  let kg;
  let lb;

  if (currentWeightUnit === "kg") {

    kg = value;
    lb = value * 2.2046226218;

  } else {

    lb = value;
    kg = value / 2.2046226218;

  }

  data.weights.push({

    id: generateId(),

    date,

    kg,

    lb,

    notes

  });

  data.weights.sort(
    (a, b) =>
      new Date(a.date) -
      new Date(b.date)
  );

  saveData();

  renderAll();

  document.getElementById("weightValue").value = "";

  document.getElementById("weightNotes").value = "";

  showToast("Weight saved.");

}


function renderWeightHistory() {

  const container =
    document.getElementById("weightHistory");

  if (!data.weights.length) {

    container.innerHTML = `
      <div class="empty">
        <div class="empty-icon">⚖️</div>
        <p>No weight entries yet.</p>
      </div>
    `;

    return;
  }

  const entries =
    [...data.weights].reverse();

  container.innerHTML =
    entries.map(weight => {

      return `

        <div class="weight-entry">

          <div>

            <strong>
              ${weight.kg.toFixed(1)} KG
            </strong>

            <div class="exercise-detail">
              ${weight.lb.toFixed(1)} LB
            </div>

            ${
              weight.notes
                ? `
                  <div class="exercise-detail">
                    ${escapeHtml(weight.notes)}
                  </div>
                `
                : ""
            }

          </div>

          <div style="display:flex;align-items:center;gap:8px;">

            <span class="muted">
              ${formatDate(weight.date)}
            </span>

            <button
              class="btn btn-small btn-danger"
              onclick="deleteWeight('${weight.id}')"
            >
              ×
            </button>

          </div>

        </div>

      `;

    }).join("");

}


function deleteWeight(id) {

  data.weights =
    data.weights.filter(
      weight => weight.id !== id
    );

  saveData();

  renderAll();

  showToast("Weight entry deleted.");

}


/* =========================================================
   EXERCISE LIBRARY
========================================================= */

const exerciseLibrary = {

  "Chest": [
    "Barbell Bench Press",
    "Incline Barbell Bench Press",
    "Dumbbell Bench Press",
    "Incline Dumbbell Press",
    "Cable Fly",
    "Chest Fly Machine",
    "Push-Ups",
    "Dips"
  ],

  "Back": [
    "Pull-Ups",
    "Lat Pulldown",
    "Barbell Row",
    "Dumbbell Row",
    "Seated Cable Row",
    "Chest-Supported Row",
    "T-Bar Row",
    "Straight-Arm Pulldown"
  ],

  "Shoulders": [
    "Overhead Press",
    "Dumbbell Shoulder Press",
    "Arnold Press",
    "Lateral Raises",
    "Front Raises",
    "Reverse Fly",
    "Face Pulls"
  ],

  "Biceps": [
    "Barbell Curl",
    "EZ-Bar Curl",
    "Dumbbell Curl",
    "Hammer Curl",
    "Incline Dumbbell Curl",
    "Preacher Curl",
    "Cable Curl"
  ],

  "Triceps": [
    "Tricep Pushdown",
    "Overhead Tricep Extension",
    "Skull Crushers",
    "Close-Grip Bench Press",
    "Dips",
    "Dumbbell Kickbacks"
  ],

  "Quads": [
    "Barbell Squat",
    "Front Squat",
    "Leg Press",
    "Hack Squat",
    "Bulgarian Split Squat",
    "Walking Lunges",
    "Leg Extension"
  ],

  "Hamstrings": [
    "Romanian Deadlift",
    "Stiff-Leg Deadlift",
    "Lying Leg Curl",
    "Seated Leg Curl",
    "Good Mornings",
    "Nordic Curl"
  ],

  "Glutes": [
    "Hip Thrust",
    "Barbell Hip Thrust",
    "Glute Bridge",
    "Bulgarian Split Squat",
    "Cable Kickback",
    "Walking Lunges"
  ],

  "Calves": [
    "Standing Calf Raise",
    "Seated Calf Raise",
    "Leg Press Calf Raise",
    "Single-Leg Calf Raise"
  ],

  "Abs": [
    "Cable Crunch",
    "Hanging Leg Raise",
    "Knee Raise",
    "Ab Wheel Rollout",
    "Plank",
    "Decline Sit-Up"
  ],

  "Full Body": [
    "Deadlift",
    "Clean & Press",
    "Kettlebell Swing",
    "Farmer's Walk",
    "Thrusters",
    "Burpees"
  ]

};


function renderSuggestions() {

  const container =
    document.getElementById("suggestionsContainer");

  container.innerHTML =
    Object.entries(exerciseLibrary)
      .map(([zone, exercises]) => {

        return `

          <div class="card" style="margin-bottom:18px;">

            <div class="card-header">

              <h2>
                ${escapeHtml(zone)}
              </h2>

              <span class="muted">
                ${exercises.length} exercises
              </span>

            </div>

            ${exercises.map(exercise => {

              return `

                <div class="suggestion">

                  <div>
                    <div class="suggestion-name">
                      ${escapeHtml(exercise)}
                    </div>

                    <div class="suggestion-zone">
                      ${escapeHtml(zone)}
                    </div>
                  </div>

                  <button
                    class="btn btn-small"
                    onclick="copyExercise('${escapeAttribute(exercise)}')"
                  >
                    Copy
                  </button>

                </div>

              `;

            }).join("")}

          </div>

        `;

      }).join("");

}


function copyExercise(name) {

  navigator.clipboard
    .writeText(name)
    .then(() => {

      showToast(
        `${name} copied to clipboard.`
      );

    })
    .catch(() => {

      showToast("Exercise copied.");

    });

}


/* =========================================================
   EXPORT / IMPORT
========================================================= */

function exportData() {

  const json =
    JSON.stringify(data, null, 2);

  const blob =
    new Blob(
      [json],
      { type: "application/json" }
    );

  const url =
    URL.createObjectURL(blob);

  const link =
    document.createElement("a");

  link.href = url;

  link.download =
    "gymtrack-backup.json";

  link.click();

  URL.revokeObjectURL(url);

  showToast("Data exported.");

}


function importData(event) {

  const file =
    event.target.files[0];

  if (!file) return;

  const reader =
    new FileReader();

  reader.onload = function(e) {

    try {

      const imported =
        JSON.parse(e.target.result);

      if (
        !imported.templates ||
        !imported.weights
      ) {

        throw new Error(
          "Invalid GymTrack backup."
        );

      }

      data = imported;

      saveData();

      applyTheme();

      renderAll();

      showToast(
        "Data imported successfully."
      );

    } catch (error) {

      alert(
        "Could not import this file. " +
        "Make sure it is a GymTrack JSON backup."
      );

    }

  };

  reader.readAsText(file);

}


/* =========================================================
   UTILITIES
========================================================= */

function formatDate(dateString) {

  const date =
    new Date(dateString);

  return date.toLocaleDateString(
    undefined,
    {
      month: "short",
      day: "numeric",
      year: "numeric"
    }
  );

}


function escapeHtml(value) {

  return String(value)
    .replaceAll("&", "&amp;")
    .replaceAll("<", "&lt;")
    .replaceAll(">", "&gt;")
    .replaceAll('"', "&quot;")
    .replaceAll("'", "&#039;");

}


function escapeAttribute(value) {

  return escapeHtml(value)
    .replaceAll("`", "&#096;");
}


function showToast(message) {

  const toast =
    document.getElementById("toast");

  toast.textContent = message;

  toast.classList.add("show");

  setTimeout(() => {

    toast.classList.remove("show");

  }, 2500);

}


/* =========================================================
   CLOSE MODALS WHEN CLICKING OUTSIDE
========================================================= */

document.addEventListener("click", function(event) {

  if (
    event.target.classList.contains(
      "modal-overlay"
    )
  ) {

    event.target.classList.remove("show");

  }

});


/* =========================================================
   ESCAPE KEY
========================================================= */

document.addEventListener("keydown", function(event) {

  if (event.key === "Escape") {

    document
      .querySelectorAll(".modal-overlay.show")
      .forEach(modal => {

        modal.classList.remove("show");

      });

  }

});

</script>

</body>
</html>
