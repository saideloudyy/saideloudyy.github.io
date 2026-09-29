<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PulseFit - Modern Workout Tracker</title>
  <style>
    :root {
      --bg: #090d16;
      --panel: #131b2e;
      --panel-hover: #1c2742;
      --card: #182238;
      --border: #263554;
      --text: #f1f5f9;
      --muted: #8e9bb0;
      --accent: #00f2fe;
      --accent-gradient: linear-gradient(135deg, #00f2fe 0%, #4facfe 100%);
      --accent-glow: rgba(0, 242, 254, 0.25);
      --success: #10b981;
      --danger: #ff4b4b;
      --radius: 18px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      background: var(--bg);
      color: var(--text);
      min-height: 100vh;
      padding-bottom: 90px;
    }

    /* TOP BAR */
    header {
      background: rgba(19, 27, 46, 0.8);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
      position: sticky;
      top: 0;
      z-index: 100;
      padding: 16px 24px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 12px;
      font-size: 20px;
      font-weight: 800;
      letter-spacing: -0.5px;
    }

    .brand-badge {
      background: var(--accent-gradient);
      color: #000;
      width: 36px;
      height: 36px;
      border-radius: 10px;
      display: grid;
      place-items: center;
      font-weight: 900;
      box-shadow: 0 0 15px var(--accent-glow);
    }

    .header-actions {
      display: flex;
      gap: 10px;
    }

    /* FLOATING BOTTOM NAV */
    nav.bottom-nav {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(24, 34, 56, 0.85);
      backdrop-filter: blur(16px);
      border: 1px solid var(--border);
      padding: 8px 12px;
      border-radius: 40px;
      display: flex;
      gap: 8px;
      z-index: 200;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
    }

    nav.bottom-nav button {
      background: transparent;
      border: 0;
      color: var(--muted);
      padding: 10px 18px;
      border-radius: 25px;
      font-weight: 600;
      font-size: 14px;
      cursor: pointer;
      transition: all 0.2s ease;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    nav.bottom-nav button.active {
      background: var(--accent-gradient);
      color: #000;
      box-shadow: 0 0 15px var(--accent-glow);
    }

    /* MAIN CONTAINER */
    main {
      max-width: 1000px;
      margin: 0 auto;
      padding: 24px 16px;
    }

    .section {
      display: none;
    }

    .section.active {
      display: block;
    }

    /* BUTTONS */
    .btn {
      background: var(--panel-hover);
      color: var(--text);
      border: 1px solid var(--border);
      padding: 10px 18px;
      border-radius: 12px;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .btn:hover {
      border-color: var(--muted);
    }

    .btn-accent {
      background: var(--accent-gradient);
      color: #000;
      border: none;
      box-shadow: 0 0 15px var(--accent-glow);
    }

    .btn-accent:hover {
      opacity: 0.95;
    }

    .btn-danger {
      color: var(--danger);
      border-color: rgba(255, 75, 75, 0.3);
      background: rgba(255, 75, 75, 0.1);
    }

    .btn-sm {
      padding: 6px 12px;
      font-size: 12px;
      border-radius: 8px;
    }

    /* CARDS & LAYOUT */
    .grid-2 {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 16px;
    }

    .card {
      background: var(--panel);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 20px;
      margin-bottom: 16px;
    }

    .stat-banner {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
      gap: 12px;
      margin-bottom: 24px;
    }

    .stat-tile {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 16px;
    }

    .stat-tile label {
      font-size: 12px;
      color: var(--muted);
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    .stat-tile .val {
      font-size: 26px;
      font-weight: 800;
      margin-top: 6px;
      color: var(--accent);
    }

    /* FORMS */
    .form-group {
      margin-bottom: 14px;
    }

    .form-group label {
      display: block;
      font-size: 12px;
      color: var(--muted);
      margin-bottom: 6px;
      text-transform: uppercase;
    }

    input, select, textarea {
      width: 100%;
      background: var(--bg);
      border: 1px solid var(--border);
      color: var(--text);
      padding: 10px 14px;
      border-radius: 10px;
      outline: none;
    }

    input:focus, select:focus, textarea:focus {
      border-color: var(--accent);
    }

    /* LISTS & SETS */
    .exercise-block {
      background: var(--card);
      border-radius: 12px;
      padding: 14px;
      margin-top: 10px;
    }

    .set-row {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr auto;
      gap: 8px;
      align-items: center;
      margin-top: 8px;
    }

    /* MODAL */
    .modal-backdrop {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0, 0, 0, 0.7);
      backdrop-filter: blur(8px);
      z-index: 500;
      align-items: center;
      justify-content: center;
      padding: 16px;
    }

    .modal-backdrop.open {
      display: flex;
    }

    .modal-box {
      background: var(--panel);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      width: 100%;
      max-width: 600px;
      max-height: 85vh;
      overflow-y: auto;
      padding: 24px;
    }

    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 16px;
    }

    .close-btn {
      background: transparent;
      border: none;
      color: var(--muted);
      font-size: 20px;
      cursor: pointer;
    }

    /* TOAST */
    .toast {
      position: fixed;
      top: 20px;
      right: 20px;
      background: var(--accent-gradient);
      color: #000;
      font-weight: 700;
      padding: 12px 20px;
      border-radius: 30px;
      transform: translateY(-50px);
      opacity: 0;
      transition: all 0.3s ease;
      z-index: 1000;
    }

    .toast.visible {
      transform: translateY(0);
      opacity: 1;
    }
  </style>
</head>
<body>

  <header>
    <div class="brand">
      <div class="brand-badge">P</div>
      <span>PulseFit</span>
    </div>
    <div class="header-actions">
      <button class="btn btn-sm" onclick="exportJSON()">Export</button>
      <button class="btn btn-sm" onclick="document.getElementById('importFile').click()">Import</button>
      <input type="file" id="importFile" style="display:none" onchange="importJSON(event)" />
    </div>
  </header>

  <main>
    <!-- DASHBOARD VIEW -->
    <section id="dashboardView" class="section active">
      <div class="stat-banner">
        <div class="stat-tile">
          <label>Workouts</label>
          <div class="val" id="statWorkouts">0</div>
        </div>
        <div class="stat-tile">
          <label>Templates</label>
          <div class="val" id="statTemplates">0</div>
        </div>
        <div class="stat-tile">
          <label>Current Weight</label>
          <div class="val" id="statWeight">--</div>
        </div>
      </div>

      <div class="card">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:12px;">
          <h3>Quick Start Workouts</h3>
          <button class="btn btn-accent btn-sm" onclick="openTemplateModal()">+ New Routine</button>
        </div>
        <div id="quickTemplatesList"></div>
      </div>
    </section>

    <!-- ROUTINES VIEW -->
    <section id="routinesView" class="section">
      <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:16px;">
        <h2>Workout Routines</h2>
        <button class="btn btn-accent" onclick="openTemplateModal()">+ Create Routine</button>
      </div>
      <div id="routinesList"></div>
    </section>

    <!-- WEIGHT TRACKER VIEW -->
    <section id="weightView" class="section">
      <div class="grid-2">
        <div class="card">
          <h3>Log Weight</h3>
          <div class="form-group" style="margin-top:12px;">
            <label>Date</label>
            <input type="date" id="weightDate" />
          </div>
          <div class="form-group">
            <label>Weight (kg)</label>
            <input type="number" step="0.1" id="weightVal" placeholder="75.5" />
          </div>
          <button class="btn btn-accent" style="width:100%" onclick="saveWeightLog()">Record Entry</button>
        </div>

        <div class="card">
          <h3>Weight Progress</h3>
          <canvas id="weightCanvas" height="150" style="width:100%; margin-top:12px;"></canvas>
          <div id="weightHistory" style="margin-top:16px; max-height: 180px; overflow-y:auto;"></div>
        </div>
      </div>
    </section>
  </main>

  <!-- NAVIGATION -->
  <nav class="bottom-nav">
    <button class="active" onclick="switchTab('dashboardView', this)">Dashboard</button>
    <button onclick="switchTab('routinesView', this)">Routines</button>
    <button onclick="switchTab('weightView', this)">Weight</button>
  </nav>

  <!-- TEMPLATE BUILDER MODAL -->
  <div class="modal-backdrop" id="templateModal">
    <div class="modal-box">
      <div class="modal-header">
        <h3 id="modalTitle">Create Routine</h3>
        <button class="close-btn" onclick="closeModal('templateModal')">&times;</button>
      </div>
      <div class="form-group">
        <label>Routine Name</label>
        <input type="text" id="routineNameInput" placeholder="Upper Body Power" />
      </div>
      <div id="builderExercises"></div>
      <button class="btn" style="width:100%; margin-top:10px;" onclick="addExerciseToBuilder()">+ Add Exercise</button>
      <div style="display:flex; justify-content:flex-end; gap:8px; margin-top:20px;">
        <button class="btn" onclick="closeModal('templateModal')">Cancel</button>
        <button class="btn btn-accent" onclick="saveRoutine()">Save Routine</button>
      </div>
    </div>
  </div>

  <!-- ACTIVE WORKOUT MODAL -->
  <div class="modal-backdrop" id="workoutModal">
    <div class="modal-box">
      <div class="modal-header">
        <h3 id="activeWorkoutTitle">Session</h3>
        <button class="close-btn" onclick="closeModal('workoutModal')">&times;</button>
      </div>
      <div id="activeWorkoutBody"></div>
      <button class="btn btn-accent" style="width:100%; margin-top:20px;" onclick="finishWorkoutSession()">Finish Workout</button>
    </div>
  </div>

  <div class="toast" id="toast">Changes saved!</div>

  <script>
    const STORAGE_KEY = "pulsefit_data";
    let state = loadData();
    let currentBuilder = { id: null, name: "", exercises: [] };

    function loadData() {
      const defaultState = {
        routines: [
          {
            id: "1",
            name: "Upper Body Hypertrophy",
            exercises: [
              { name: "Bench Press", sets: 3, reps: 10, weight: 60 },
              { name: "Incline Dumbbell Press", sets: 3, reps: 12, weight: 20 }
            ]
          }
        ],
        weights: [],
        completed: 0
      };
      const saved = localStorage.getItem(STORAGE_KEY);
      return saved ? JSON.parse(saved) : defaultState;
    }

    function saveData() {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
      render();
    }

    function notify(msg) {
      const toast = document.getElementById("toast");
      toast.textContent = msg;
      toast.classList.add("visible");
      setTimeout(() => toast.classList.remove("visible"), 2500);
    }

    function switchTab(viewId, btn) {
      document.querySelectorAll(".section").forEach(s => s.classList.remove("active"));
      document.querySelectorAll("nav.bottom-nav button").forEach(b => b.classList.remove("active"));
      document.getElementById(viewId).classList.add("active");
      btn.classList.add("active");
      if(viewId === 'weightView') renderWeightChart();
    }

    function openModal(id) { document.getElementById(id).classList.add("open"); }
    function closeModal(id) { document.getElementById(id).classList.remove("open"); }

    /* ROUTINES & BUILDER */
    function openTemplateModal(id = null) {
      if (id) {
        const found = state.routines.find(r => r.id === id);
        currentBuilder = JSON.parse(JSON.stringify(found));
      } else {
        currentBuilder = { id: Date.now().toString(), name: "", exercises: [] };
      }
      document.getElementById("routineNameInput").value = currentBuilder.name;
      renderBuilderExercises();
      openModal("templateModal");
    }

    function renderBuilderExercises() {
      const container = document.getElementById("builderExercises");
      container.innerHTML = currentBuilder.exercises.map((ex, i) => `
        <div class="exercise-block">
          <div class="form-group">
            <label>Exercise Name</label>
            <input type="text" value="${ex.name}" onchange="currentBuilder.exercises[${i}].name = this.value" placeholder="Exercise Title" />
          </div>
          <div style="display:grid; grid-template-columns: 1fr 1fr 1fr; gap:8px;">
            <div><label>Sets</label><input type="number" value="${ex.sets}" onchange="currentBuilder.exercises[${i}].sets = Number(this.value)" /></div>
            <div><label>Reps</label><input type="number" value="${ex.reps}" onchange="currentBuilder.exercises[${i}].reps = Number(this.value)" /></div>
            <div><label>Kg</label><input type="number" value="${ex.weight}" onchange="currentBuilder.exercises[${i}].weight = Number(this.value)" /></div>
          </div>
        </div>
      `).join("");
    }

    function addExerciseToBuilder() {
      currentBuilder.exercises.push({ name: "", sets: 3, reps: 10, weight: 0 });
      renderBuilderExercises();
    }

    function saveRoutine() {
      currentBuilder.name = document.getElementById("routineNameInput").value || "Untitled Routine";
      const idx = state.routines.findIndex(r => r.id === currentBuilder.id);
      if (idx > -1) state.routines[idx] = currentBuilder;
      else state.routines.push(currentBuilder);
      saveData();
      closeModal("templateModal");
      notify("Routine Saved");
    }

    function deleteRoutine(id) {
      state.routines = state.routines.filter(r => r.id !== id);
      saveData();
      notify("Routine Deleted");
    }

    /* ACTIVE WORKOUT EXECUTION */
    function startWorkout(id) {
      const routine = state.routines.find(r => r.id === id);
      if (!routine) return;
      document.getElementById("activeWorkoutTitle").textContent = routine.name;
      
      const body = document.getElementById("activeWorkoutBody");
      body.innerHTML = routine.exercises.map(ex => `
        <div class="exercise-block">
          <strong>${ex.name}</strong>
          <div class="set-row">
            <div><label>Target Sets</label><div>${ex.sets}</div></div>
            <div><label>Reps</label><input type="number" value="${ex.reps}" /></div>
            <div><label>Weight (kg)</label><input type="number" value="${ex.weight}" /></div>
            <div><label>Done</label><input type="checkbox" style="width:20px; height:20px;" /></div>
          </div>
        </div>
      `).join("");
      
      openModal("workoutModal");
    }

    function finishWorkoutSession() {
      state.completed += 1;
      saveData();
      closeModal("workoutModal");
      notify("Workout Logged! 🎉");
    }

    /* WEIGHT LOGGING & CHART */
    function saveWeightLog() {
      const val = parseFloat(document.getElementById("weightVal").value);
      const date = document.getElementById("weightDate").value;
      if (!val || !date) return;

      state.weights.push({ date, weight: val });
      state.weights.sort((a, b) => new Date(a.date) - new Date(b.date));
      saveData();
      notify("Weight Logged");
    }

    function renderWeightChart() {
      const canvas = document.getElementById("weightCanvas");
      const ctx = canvas.getContext("2d");
      canvas.width = canvas.parentElement.clientWidth - 40;
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      if (state.weights.length < 2) {
        ctx.fillStyle = "#8e9bb0";
        ctx.font = "12px sans-serif";
        ctx.fillText("Log at least 2 entries to display chart", 10, 75);
        return;
      }

      const padding = 20;
      const pts = state.weights.map(w => w.weight);
      const min = Math.min(...pts) - 1;
      const max = Math.max(...pts) + 1;

      ctx.beginPath();
      ctx.strokeStyle = "#00f2fe";
      ctx.lineWidth = 2;

      pts.forEach((pt, i) => {
        const x = padding + (i / (pts.length - 1)) * (canvas.width - padding * 2);
        const y = canvas.height - padding - ((pt - min) / (max - min)) * (canvas.height - padding * 2);
        if (i === 0) ctx.moveTo(x, y);
        else ctx.lineTo(x, y);
      });
      ctx.stroke();
    }

    /* RENDER ALL VIEWS */
    function render() {
      document.getElementById("statWorkouts").textContent = state.completed;
      document.getElementById("statTemplates").textContent = state.routines.length;
      const latestW = state.weights[state.weights.length - 1];
      document.getElementById("statWeight").textContent = latestW ? `${latestW.weight} kg` : "--";

      // Render Routines
      const listHtml = state.routines.map(r => `
        <div class="card" style="margin-bottom:12px;">
          <div style="display:flex; justify-content:space-between; align-items:center;">
            <div>
              <h4 style="font-size:16px;">${r.name}</h4>
              <p style="color:var(--muted); font-size:12px; margin-top:4px;">${r.exercises.length} Exercises</p>
            </div>
            <div style="display:flex; gap:6px;">
              <button class="btn btn-accent btn-sm" onclick="startWorkout('${r.id}')">Start</button>
              <button class="btn btn-sm" onclick="openTemplateModal('${r.id}')">Edit</button>
              <button class="btn btn-danger btn-sm" onclick="deleteRoutine('${r.id}')">&times;</button>
            </div>
          </div>
        </div>
      `).join("");

      document.getElementById("quickTemplatesList").innerHTML = listHtml || "<p style='color:var(--muted)'>No routines defined yet.</p>";
      document.getElementById("routinesList").innerHTML = listHtml || "<p style='color:var(--muted)'>No routines defined yet.</p>";

      // Weight history
      document.getElementById("weightHistory").innerHTML = [...state.weights].reverse().map(w => `
        <div style="display:flex; justify-content:space-between; padding:8px 0; border-bottom:1px solid var(--border); font-size:13px;">
          <span>${w.date}</span>
          <strong style="color:var(--accent);">${w.weight} kg</strong>
        </div>
      `).join("");
    }

    /* EXPORT & IMPORT */
    function exportJSON() {
      const blob = new Blob([JSON.stringify(state, null, 2)], { type: "application/json" });
      const a = document.createElement("a");
      a.href = URL.createObjectURL(blob);
      a.download = `pulsefit_data.json`;
      a.click();
    }

    function importJSON(e) {
      const file = e.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = (evt) => {
        try {
          state = JSON.parse(evt.target.result);
          saveData();
          notify("Data Restored");
        } catch (err) {
          alert("Invalid File Format");
        }
      };
      reader.readAsText(file);
    }

    // Init
    document.getElementById("weightDate").value = new Date().toISOString().split("T")[0];
    render();
  </script>
</body>
</html>
