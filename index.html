<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Thought Record · CBT Worksheet</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=DM+Sans:wght@300;400;500;700&family=Allura&family=Playfair+Display:wght@600;700&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<style>
:root {
  --night: #0d1124;
  --deep: #1a1f3e;
  --dusk: #2e2450;
  --lavender: #c9b8e8;
  --blush: #e8c8d4;
  --cream: #f5f0ea;
  --gold: #d4a96a;
  --moon: #f0e8d0;
  --text: #e8e0f0;
  --muted: rgba(232,224,240,0.45);
  --card: rgba(255,255,255,0.04);
  --card-border: rgba(255,255,255,0.08);
  --radius: 18px;
}

* { margin:0; padding:0; box-sizing:border-box; }

body {
  font-family: 'DM Sans', sans-serif;
  background: var(--night);
  color: var(--text);
  min-height: 100vh;
  overflow-x: hidden;
  padding: 2rem 1rem;
}

/* ── CANVAS STARFIELD ── */
#stars-canvas {
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100%;
  pointer-events: none;
  z-index: 0;
}

/* ── MAIN CONTAINER ── */
.container {
  max-width: 700px;
  margin: 0 auto;
  position: relative;
  z-index: 1;
}

/* ── HEADER ── */
.header {
  text-align: center;
  margin-bottom: 3rem;
}

.title {
  font-family: 'Allura', cursive;
  font-size: 3rem;
  color: var(--moon);
  margin-bottom: 0.5rem;
}

/* ── NAVIGATION TABS ── */
.nav-tabs {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 2rem;
  border-bottom: 1px solid var(--card-border);
  flex-wrap: wrap;
}

.nav-tab {
  background: none;
  border: none;
  color: var(--muted);
  font-family: 'DM Sans', sans-serif;
  font-size: 0.95rem;
  font-weight: 500;
  padding: 0.75rem 1.25rem;
  cursor: pointer;
  border-bottom: 2px solid transparent;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.nav-tab:hover {
  color: var(--lavender);
}

.nav-tab.active {
  color: var(--lavender);
  border-bottom-color: var(--lavender);
}

.nav-tab svg {
  width: 18px;
  height: 18px;
}

/* ── TAB CONTENT ── */
.tab-content {
  display: none;
}

.tab-content.active {
  display: block;
}

/* ── CARD ── */
.card {
  background: var(--card);
  border: 1px solid var(--card-border);
  border-radius: var(--radius);
  padding: 2rem;
  backdrop-filter: blur(20px);
  margin-bottom: 1.5rem;
}

/* ── FORM SECTIONS ── */
.section {
  margin-bottom: 2rem;
}

.section:last-child {
  margin-bottom: 0;
}

.section-label {
  font-family: 'Playfair Display', serif;
  font-size: 1.4rem;
  font-weight: 700;
  color: var(--lavender);
  margin-bottom: 0.75rem;
  display: block;
  letter-spacing: 0.3px;
}

.helper-text {
  font-size: 0.875rem;
  color: var(--muted);
  margin-bottom: 0.5rem;
  font-style: italic;
}

/* ── INPUTS ── */
textarea, input[type="text"] {
  width: 100%;
  background: rgba(255,255,255,0.02);
  border: 1px solid var(--card-border);
  border-radius: 12px;
  padding: 1rem;
  color: var(--text);
  font-family: 'DM Sans', sans-serif;
  font-size: 1rem;
  line-height: 1.6;
  resize: vertical;
  transition: border-color 0.3s ease;
}

textarea {
  min-height: 100px;
}

textarea:focus, input:focus {
  outline: none;
  border-color: var(--lavender);
}

textarea::placeholder, input::placeholder {
  color: var(--muted);
}

/* ── EMOTION INTENSITY ── */
.emotion-row {
  display: flex;
  gap: 1rem;
  align-items: flex-start;
}

.emotion-row > div:first-child {
  flex: 2;
}

.emotion-row > div:last-child {
  flex: 1;
}

.intensity-label {
  font-size: 0.875rem;
  color: var(--muted);
  margin-bottom: 0.5rem;
  display: block;
}

input[type="range"] {
  width: 100%;
  height: 6px;
  background: rgba(255,255,255,0.1);
  border-radius: 3px;
  outline: none;
  -webkit-appearance: none;
  margin: 0.5rem 0;
}

input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 20px;
  height: 20px;
  background: var(--lavender);
  border-radius: 50%;
  cursor: pointer;
}

input[type="range"]::-moz-range-thumb {
  width: 20px;
  height: 20px;
  background: var(--lavender);
  border-radius: 50%;
  cursor: pointer;
  border: none;
}

.intensity-value {
  text-align: center;
  color: var(--lavender);
  font-size: 1.5rem;
  font-weight: 500;
  margin-top: 0.5rem;
}

/* ── EVIDENCE GRID ── */
.evidence-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  margin-bottom: 2rem;
}

@media (max-width: 600px) {
  .evidence-grid {
    grid-template-columns: 1fr;
  }
}

.evidence-box {
  background: rgba(255,255,255,0.02);
  border: 1px solid var(--card-border);
  border-radius: 12px;
  padding: 1.5rem;
}

.evidence-title {
  font-family: 'Playfair Display', serif;
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--blush);
  margin-bottom: 0.75rem;
}

.evidence-box.against .evidence-title {
  color: var(--gold);
}

/* ── DISTORTIONS ── */
.distortion-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-top: 0.5rem;
}

.distortion-tag {
  background: rgba(201,184,232,0.1);
  border: 1px solid rgba(201,184,232,0.2);
  color: var(--lavender);
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.875rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.distortion-tag:hover {
  background: rgba(201,184,232,0.2);
  border-color: var(--lavender);
}

.distortion-tag.selected {
  background: var(--lavender);
  color: var(--night);
  border-color: var(--lavender);
}

/* ── EXPANDABLE DISTORTION INFO ── */
.distortion-info-trigger {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  color: var(--muted);
  font-size: 0.875rem;
  cursor: pointer;
  margin-top: 0.75rem;
  padding: 0.5rem 0.75rem;
  border-radius: 8px;
  transition: all 0.2s ease;
}

.distortion-info-trigger:hover {
  color: var(--lavender);
  background: rgba(201,184,232,0.05);
}

.distortion-info-trigger svg {
  width: 16px;
  height: 16px;
  transition: transform 0.3s ease;
}

.distortion-info-trigger.expanded svg {
  transform: rotate(180deg);
}

.distortion-details {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.4s ease;
  margin-top: 0.5rem;
}

.distortion-details.expanded {
  max-height: 2000px;
}

.distortion-item {
  background: rgba(255,255,255,0.02);
  border: 1px solid var(--card-border);
  border-radius: 10px;
  padding: 1rem;
  margin-bottom: 0.75rem;
}

.distortion-item:last-child {
  margin-bottom: 0;
}

.distortion-name {
  font-family: 'Playfair Display', serif;
  font-weight: 600;
  color: var(--lavender);
  font-size: 1rem;
  margin-bottom: 0.5rem;
}

.distortion-description {
  font-size: 0.875rem;
  color: var(--text);
  line-height: 1.6;
  margin-bottom: 0.75rem;
}

.distortion-example {
  font-size: 0.85rem;
  color: var(--muted);
  font-style: italic;
  line-height: 1.5;
  padding-left: 1rem;
  border-left: 2px solid var(--card-border);
}

/* ── CONCLUSION HIGHLIGHT ── */
.conclusion-box {
  background: linear-gradient(135deg, rgba(201,184,232,0.1) 0%, rgba(232,200,212,0.1) 100%);
  border: 2px solid var(--lavender);
  border-radius: 12px;
  padding: 1.5rem;
}

/* ── ACTION BUTTONS ── */
.actions {
  display: flex;
  gap: 1rem;
  margin-top: 2rem;
  justify-content: center;
  flex-wrap: wrap;
}

.btn {
  padding: 1rem 2rem;
  border-radius: 12px;
  border: none;
  font-family: 'DM Sans', sans-serif;
  font-size: 1rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
}

.btn-primary {
  background: linear-gradient(135deg, var(--lavender) 0%, var(--blush) 100%);
  color: var(--night);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(201,184,232,0.3);
}

.btn-secondary {
  background: rgba(255,255,255,0.05);
  color: var(--text);
  border: 1px solid var(--card-border);
}

.btn-secondary:hover {
  background: rgba(255,255,255,0.08);
  border-color: var(--lavender);
}

/* ── SVG ICON BUTTONS ── */
.icon-btn {
  background: rgba(255,255,255,0.05);
  border: 1px solid var(--card-border);
  border-radius: 8px;
  padding: 0.5rem 0.75rem;
  cursor: pointer;
  transition: all 0.2s ease;
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 0.875rem;
  color: var(--text);
}

.icon-btn:hover {
  background: rgba(255,255,255,0.1);
  border-color: var(--lavender);
  color: var(--lavender);
}

.icon-btn svg {
  width: 16px;
  height: 16px;
  stroke: currentColor;
  fill: none;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.icon-btn-delete {
  border-color: rgba(232,200,212,0.3);
}

.icon-btn-delete:hover {
  border-color: var(--blush);
  color: var(--blush);
}

/* ── SAVED MESSAGE ── */
.saved-msg {
  position: fixed;
  top: 2rem;
  right: 2rem;
  background: var(--lavender);
  color: var(--night);
  padding: 1rem 1.5rem;
  border-radius: 12px;
  font-weight: 500;
  opacity: 0;
  transform: translateY(-20px);
  transition: all 0.3s ease;
  z-index: 1000;
  box-shadow: 0 8px 20px rgba(0,0,0,0.3);
}

.saved-msg.show {
  opacity: 1;
  transform: translateY(0);
}

/* ── HISTORY SECTION ── */
.no-records {
  text-align: center;
  color: var(--muted);
  padding: 2rem;
  font-style: italic;
}

.record-card {
  background: var(--card);
  border: 1px solid var(--card-border);
  border-radius: var(--radius);
  padding: 1.5rem;
  margin-bottom: 1rem;
  backdrop-filter: blur(20px);
}

.record-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid var(--card-border);
}

.record-date {
  font-family: 'Cormorant Garamond', serif;
  color: var(--muted);
  font-size: 0.95rem;
}

.record-actions {
  display: flex;
  gap: 0.5rem;
}

.record-content {
  display: grid;
  gap: 1rem;
}

.record-field {
  display: grid;
  gap: 0.4rem;
}

.record-field-label {
  font-family: 'Playfair Display', serif;
  font-weight: 600;
  color: var(--lavender);
  font-size: 0.95rem;
}

.record-field-value {
  color: var(--text);
  line-height: 1.6;
  font-size: 0.95rem;
}

.record-distortions {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
}

.record-distortion-tag {
  background: rgba(201,184,232,0.15);
  border: 1px solid rgba(201,184,232,0.25);
  color: var(--lavender);
  padding: 0.35rem 0.75rem;
  border-radius: 16px;
  font-size: 0.8rem;
}

/* ── EDIT MODE ── */
.edit-mode {
  background: rgba(201,184,232,0.05);
  border-color: var(--lavender);
}

.edit-form {
  display: none;
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid var(--card-border);
}

.edit-form.active {
  display: block;
}

.edit-form textarea {
  margin-bottom: 0.75rem;
}

.edit-actions {
  display: flex;
  gap: 0.5rem;
  margin-top: 1rem;
}

/* ── INSIGHTS & STATS ── */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 1rem;
  margin-bottom: 2rem;
}

.stat-card {
  background: rgba(255,255,255,0.02);
  border: 1px solid var(--card-border);
  border-radius: 12px;
  padding: 1.5rem;
  text-align: center;
}

.stat-value {
  font-family: 'Playfair Display', serif;
  font-size: 2rem;
  font-weight: 700;
  color: var(--lavender);
  margin-bottom: 0.5rem;
}

.stat-label {
  font-size: 0.875rem;
  color: var(--muted);
}

.chart-container {
  background: rgba(255,255,255,0.02);
  border: 1px solid var(--card-border);
  border-radius: 12px;
  padding: 1.5rem;
  margin-bottom: 1.5rem;
  position: relative;
  height: 300px;
}

.pattern-list {
  display: grid;
  gap: 0.75rem;
}

.pattern-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: rgba(255,255,255,0.02);
  border: 1px solid var(--card-border);
  border-radius: 10px;
  padding: 1rem;
}

.pattern-name {
  font-weight: 500;
  color: var(--text);
}

.pattern-count {
  background: var(--lavender);
  color: var(--night);
  padding: 0.25rem 0.75rem;
  border-radius: 12px;
  font-size: 0.875rem;
  font-weight: 600;
}

/* ── QUICK EXAMPLES ── */
.example-card {
  background: rgba(201,184,232,0.05);
  border: 1px solid rgba(201,184,232,0.2);
  border-radius: 12px;
  padding: 1.25rem;
  margin-bottom: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.example-card:hover {
  background: rgba(201,184,232,0.1);
  border-color: var(--lavender);
  transform: translateY(-2px);
}

.example-thought {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.1rem;
  color: var(--text);
  margin-bottom: 0.75rem;
  font-style: italic;
}

.example-response {
  font-size: 0.9rem;
  color: var(--muted);
  line-height: 1.6;
}

.example-tag {
  display: inline-block;
  background: rgba(201,184,232,0.2);
  color: var(--lavender);
  padding: 0.25rem 0.75rem;
  border-radius: 12px;
  font-size: 0.75rem;
  margin-top: 0.5rem;
  font-weight: 500;
}

/* ── TOOLKIT ── */
.toolkit-grid {
  display: grid;
  gap: 1rem;
}

.toolkit-item {
  background: rgba(255,255,255,0.02);
  border: 1px solid var(--card-border);
  border-radius: 12px;
  padding: 1.5rem;
  transition: all 0.3s ease;
}

.toolkit-item:hover {
  border-color: var(--lavender);
  background: rgba(201,184,232,0.05);
}

.toolkit-title {
  font-family: 'Playfair Display', serif;
  font-weight: 600;
  color: var(--lavender);
  font-size: 1.1rem;
  margin-bottom: 0.75rem;
}

.toolkit-content {
  color: var(--text);
  line-height: 1.6;
  font-size: 0.95rem;
}

.toolkit-steps {
  list-style: none;
  padding-left: 0;
  margin-top: 0.5rem;
}

.toolkit-steps li {
  padding: 0.5rem 0;
  padding-left: 1.5rem;
  position: relative;
}

.toolkit-steps li:before {
  content: "•";
  position: absolute;
  left: 0;
  color: var(--lavender);
  font-weight: bold;
}

/* ── RESPONSIVE ── */
@media (max-width: 600px) {
  .title {
    font-size: 2.5rem;
  }
  
  .actions {
    flex-direction: column;
  }
  
  .btn {
    width: 100%;
    justify-content: center;
  }
  
  .record-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 1rem;
  }
  
  .nav-tabs {
    overflow-x: auto;
  }
}
</style>
</head>
<body>

<canvas id="stars-canvas"></canvas>

<div class="container">
  <div class="header">
    <h1 class="title">Thought Record</h1>
  </div>

  <!-- NAVIGATION -->
  <div class="nav-tabs">
    <button class="nav-tab active" onclick="switchTab('new-record')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
        <path d="M12 5v14M5 12h14"/>
      </svg>
      New Record
    </button>
    <button class="nav-tab" onclick="switchTab('history')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
        <circle cx="12" cy="12" r="10"/>
        <polyline points="12 6 12 12 16 14"/>
      </svg>
      History
    </button>
    <button class="nav-tab" onclick="switchTab('insights')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
        <line x1="12" y1="20" x2="12" y2="10"/>
        <line x1="18" y1="20" x2="18" y2="4"/>
        <line x1="6" y1="20" x2="6" y2="16"/>
      </svg>
      Insights
    </button>
    <button class="nav-tab" onclick="switchTab('examples')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
        <path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/>
        <path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/>
      </svg>
      Examples
    </button>
    <button class="nav-tab" onclick="switchTab('toolkit')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
        <rect x="3" y="3" width="18" height="18" rx="2" ry="2"/>
        <line x1="9" y1="9" x2="15" y2="9"/>
        <line x1="9" y1="15" x2="15" y2="15"/>
      </svg>
      Toolkit
    </button>
  </div>

  <!-- TAB: NEW RECORD -->
  <div id="tab-new-record" class="tab-content active">
    <div class="card">
      <!-- SITUATION -->
      <div class="section">
        <label class="section-label">Situation</label>
        <div class="helper-text">What happened? Where were you? Who was involved?</div>
        <textarea id="situation" placeholder="Describe the situation..."></textarea>
      </div>

      <!-- EMOTIONS + INTENSITY -->
      <div class="section">
        <label class="section-label">Emotions</label>
        <div class="emotion-row">
          <div>
            <div class="helper-text">What emotions did you feel?</div>
            <input type="text" id="emotions" placeholder="e.g., anxious, sad, angry...">
          </div>
          <div>
            <label class="intensity-label">Intensity (1-10)</label>
            <input type="range" id="intensity" min="1" max="10" value="5" step="1">
            <div class="intensity-value" id="intensity-value">5</div>
          </div>
        </div>
      </div>

      <!-- AUTOMATIC THOUGHTS -->
      <div class="section">
        <label class="section-label">Automatic Thoughts</label>
        <div class="helper-text">What went through your mind? What did you think would happen?</div>
        <textarea id="thoughts" placeholder="What thoughts came up..."></textarea>
      </div>

      <!-- EVIDENCE -->
      <div class="section">
        <label class="section-label">Evidence</label>
        <div class="evidence-grid">
          <div class="evidence-box for">
            <div class="evidence-title">For the Thought</div>
            <textarea id="evidence-for" placeholder="What supports this thought?"></textarea>
          </div>
          <div class="evidence-box against">
            <div class="evidence-title">Against the Thought</div>
            <textarea id="evidence-against" placeholder="What contradicts this thought?"></textarea>
          </div>
        </div>
      </div>

      <!-- COGNITIVE DISTORTIONS -->
      <div class="section">
        <label class="section-label">Cognitive Distortions</label>
        <div class="helper-text">Which thinking patterns might be present?</div>
        <div class="distortion-tags">
          <span class="distortion-tag" onclick="toggleDistortion(this)">All-or-Nothing</span>
          <span class="distortion-tag" onclick="toggleDistortion(this)">Overgeneralization</span>
          <span class="distortion-tag" onclick="toggleDistortion(this)">Catastrophizing</span>
          <span class="distortion-tag" onclick="toggleDistortion(this)">Mind Reading</span>
          <span class="distortion-tag" onclick="toggleDistortion(this)">Fortune Telling</span>
          <span class="distortion-tag" onclick="toggleDistortion(this)">Emotional Reasoning</span>
          <span class="distortion-tag" onclick="toggleDistortion(this)">Should Statements</span>
          <span class="distortion-tag" onclick="toggleDistortion(this)">Labeling</span>
          <span class="distortion-tag" onclick="toggleDistortion(this)">Personalization</span>
          <span class="distortion-tag" onclick="toggleDistortion(this)">Discounting the Positive</span>
        </div>
        
        <!-- Expandable details -->
        <div class="distortion-info-trigger" onclick="toggleDistortionInfo(this)">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
            <circle cx="12" cy="12" r="10"></circle>
            <line x1="12" y1="16" x2="12" y2="12"></line>
            <line x1="12" y1="8" x2="12.01" y2="8"></line>
          </svg>
          <span>Learn about these patterns</span>
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
            <polyline points="6 9 12 15 18 9"></polyline>
          </svg>
        </div>
        
        <div class="distortion-details" id="distortion-details">
          <div class="distortion-item">
            <div class="distortion-name">All-or-Nothing Thinking</div>
            <div class="distortion-description">Viewing situations in only two categories instead of on a continuum. Things are either perfect or terrible, with nothing in between.</div>
            <div class="distortion-example">"I'm wasting my time" — Reality: You tutor, created websites, learned French, go to therapy. Not everything has to be productive to have value.</div>
          </div>

          <div class="distortion-item">
            <div class="distortion-name">Overgeneralization</div>
            <div class="distortion-description">Making a broad conclusion based on a single incident or piece of evidence. Using words like "always," "never," "everyone."</div>
            <div class="distortion-example">"No matter how much I try, nothing works" — Reality: You CAN challenge thoughts now, use techniques like 54321 and box breathing, and have an easier time talking to people than a year ago.</div>
          </div>

          <div class="distortion-item">
            <div class="distortion-name">Catastrophizing</div>
            <div class="distortion-description">Expecting the worst possible outcome without evidence that it will happen.</div>
            <div class="distortion-example">"I will be all alone abroad. Nobody will care about me" — Reality: You can't know that. You might find people who care. It's not helpful to assume the worst.</div>
          </div>

          <div class="distortion-item">
            <div class="distortion-name">Mind Reading</div>
            <div class="distortion-description">Assuming you know what others are thinking without adequate evidence.</div>
            <div class="distortion-example">"Uliana hates me" — Reality: She smiled, helped you when sick, said she's not mad, you text about normal things, joked on the bus ride.</div>
          </div>

          <div class="distortion-item">
            <div class="distortion-name">Fortune Telling</div>
            <div class="distortion-description">Predicting the future negatively without realistic consideration of other outcomes.</div>
            <div class="distortion-example">"Nothing will work out for me" — Reality: You never know unless you try. Many people fail at first but learn. It takes time and effort, and it IS possible.</div>
          </div>

          <div class="distortion-item">
            <div class="distortion-name">Emotional Reasoning</div>
            <div class="distortion-description">Believing something is true because you feel it strongly, ignoring evidence to the contrary.</div>
            <div class="distortion-example">"I feel like all my achievements are worthless" — Reality: Your feelings are valid, but many people admire your achievements, pay for your tutoring, and value your knowledge.</div>
          </div>

          <div class="distortion-item">
            <div class="distortion-name">Should Statements</div>
            <div class="distortion-description">Having fixed rules about how you or others should behave. When reality doesn't match, you feel anxious, disappointed, or guilty.</div>
            <div class="distortion-example">"I should be able to handle everything without crying" — Reality: You're human, not a robot. Softness and vulnerability aren't weaknesses.</div>
          </div>

          <div class="distortion-item">
            <div class="distortion-name">Labeling</div>
            <div class="distortion-description">Assigning global negative traits to yourself or others. Instead of describing behavior, you label the entire person.</div>
            <div class="distortion-example">"I'm weak" or "I'm unintelligent" — Reality: You reached out for help, went to therapy despite fear, spoke up about homophobia, got up for an exam after a panic attack. That's strength, not weakness.</div>
          </div>

          <div class="distortion-item">
            <div class="distortion-name">Personalization</div>
            <div class="distortion-description">Blaming yourself for things outside your control or taking things personally when they're not about you.</div>
            <div class="distortion-example">"They didn't respond, so what I said must not matter" — Reality: Some things don't register as important to those unaffected by them. Your worth isn't tied to their response. Silence is theirs, not yours.</div>
          </div>

          <div class="distortion-item">
            <div class="distortion-name">Discounting the Positive</div>
            <div class="distortion-description">Rejecting positive experiences or achievements by insisting they "don't count" for some reason.</div>
            <div class="distortion-example">"Everyone is better than me" — Reality: People are different - some are apples, oranges, peaches. Comparison is pointless when each of us is so different. You have unique strengths: B2-C1 English self-taught, best at French in your group, 200/200 on exams, created research websites, 2+ years tutoring experience.</div>
          </div>
        </div>
      </div>

      <!-- IF A FRIEND SAID THIS -->
      <div class="section">
        <label class="section-label">If a Friend Said This...</label>
        <div class="helper-text">What would you tell a friend in this situation?</div>
        <textarea id="friend-response" placeholder="How would you respond with compassion?"></textarea>
      </div>

      <!-- BALANCED CONCLUSION -->
      <div class="section">
        <label class="section-label">Balanced Conclusion</label>
        <div class="helper-text">What's a more balanced way to view this situation?</div>
        <div class="conclusion-box">
          <textarea id="conclusion" placeholder="A more compassionate, realistic perspective..."></textarea>
        </div>
      </div>

      <!-- ACTIONS -->
      <div class="actions">
        <button class="btn btn-primary" onclick="saveRecord()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:18px;height:18px;">
            <path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"></path>
            <polyline points="17 21 17 13 7 13 7 21"></polyline>
            <polyline points="7 3 7 8 15 8"></polyline>
          </svg>
          Save Record
        </button>
        <button class="btn btn-secondary" onclick="downloadCurrentPDF()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:18px;height:18px;">
            <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"></path>
            <polyline points="7 10 12 15 17 10"></polyline>
            <line x1="12" y1="15" x2="12" y2="3"></line>
          </svg>
          Download PDF
        </button>
        <button class="btn btn-secondary" onclick="clearForm()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:18px;height:18px;">
            <polyline points="3 6 5 6 21 6"></polyline>
            <path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path>
          </svg>
          Clear Form
        </button>
      </div>
    </div>
  </div>

  <!-- TAB: HISTORY -->
  <div id="tab-history" class="tab-content">
    <div class="card">
      <label class="section-label">Past Records</label>
      <div id="records-container"></div>
    </div>
  </div>

  <!-- TAB: INSIGHTS -->
  <div id="tab-insights" class="tab-content">
    <div class="card">
      <label class="section-label">Your Progress</label>
      
      <!-- Stats -->
      <div class="stats-grid">
        <div class="stat-card">
          <div class="stat-value" id="total-records">0</div>
          <div class="stat-label">Total Records</div>
        </div>
        <div class="stat-card">
          <div class="stat-value" id="avg-intensity">-</div>
          <div class="stat-label">Avg Intensity</div>
        </div>
        <div class="stat-card">
          <div class="stat-value" id="last-week">0</div>
          <div class="stat-label">Past Week</div>
        </div>
      </div>

      <!-- Chart -->
      <div class="chart-container">
        <canvas id="intensityChart"></canvas>
      </div>

      <!-- Pattern Analysis -->
      <label class="section-label" style="margin-top: 2rem;">Common Patterns</label>
      <div class="helper-text">Distortions you identify most often</div>
      <div class="pattern-list" id="pattern-list"></div>
    </div>
  </div>

  <!-- TAB: EXAMPLES -->
  <div id="tab-examples" class="tab-content">
    <div class="card">
      <label class="section-label">Real Examples from Therapy</label>
      <div class="helper-text">Click any example to use it as a starting point</div>

      <div class="example-card" onclick="loadExample('alone-abroad')">
        <div class="example-thought">"I will be all alone abroad"</div>
        <div class="example-response">
          <strong>Challenge:</strong> Is it a fact or a thought? → You can't know that. You might find people who will care.<br>
          <strong>Helpful?</strong> → No.
        </div>
        <span class="example-tag">Catastrophizing</span>
        <span class="example-tag">Fortune Telling</span>
      </div>

      <div class="example-card" onclick="loadExample('weak')">
        <div class="example-thought">"I'm weak"</div>
        <div class="example-response">
          <strong>Evidence Against:</strong> I reached out to my friend. I decided to go to therapy despite fear. I spoke up about homophobia to my professor. I got up for an exam after a panic attack. Softness and vulnerability aren't weaknesses.
        </div>
        <span class="example-tag">Labeling</span>
        <span class="example-tag">Discounting the Positive</span>
      </div>

      <div class="example-card" onclick="loadExample('unintelligent')">
        <div class="example-thought">"I'm unintelligent"</div>
        <div class="example-response">
          <strong>Evidence Against:</strong> 200/200 English exam. B2-C1 English self-taught in one year. Best at French in my group after one year. Created research websites. 2+ years tutoring experience. Created website for mom's business.
        </div>
        <span class="example-tag">Labeling</span>
        <span class="example-tag">All-or-Nothing</span>
      </div>

      <div class="example-card" onclick="loadExample('uliana-hates')">
        <div class="example-thought">"Uliana hates me"</div>
        <div class="example-response">
          <strong>Evidence Against:</strong> She smiled at me. She helped with the exam when she had a fever. She said "I'm not mad at you." We talked after class. We text about normal things. We joked on the bus ride.
        </div>
        <span class="example-tag">Mind Reading</span>
        <span class="example-tag">Catastrophizing</span>
      </div>

      <div class="example-card" onclick="loadExample('nothing-works')">
        <div class="example-thought">"No matter how much I try, nothing works"</div>
        <div class="example-response">
          <strong>Evidence Against:</strong> I CAN challenge my thoughts now (progress). I can use techniques: 54321, box breathing, thought/fact testing. I'm getting help with diagnosed disorders that take years to treat. I have an easier time talking to people than a year ago.
        </div>
        <span class="example-tag">Overgeneralization</span>
        <span class="example-tag">Discounting the Positive</span>
      </div>

      <div class="example-card" onclick="loadExample('problems-not-real')">
        <div class="example-thought">"My pain isn't real" / "I don't have real problems"</div>
        <div class="example-response">
          <strong>Reality:</strong> I have two diagnosed anxiety disorders (SAD and GAD). 7-8 panic attacks in 5 months. I cry almost daily. I've had suicidal ideation. I'm gay in a homophobic country with homophobic family. Pain isn't something that can be measured. If it's real to me and causes me pain, then it IS real.
        </div>
        <span class="example-tag">Discounting the Positive</span>
        <span class="example-tag">Emotional Reasoning</span>
      </div>

      <div class="example-card" onclick="loadExample('nothing-matters')">
        <div class="example-thought">"Nothing I say matters"</div>
        <div class="example-response">
          <strong>Alternative View:</strong> Your worth isn't tied to whether they responded or agreed. You did the thing you were terrified to do. You expected worse than what happened - no retaliation, no judgment, no bullying. Silence stings, but the silence is theirs, not yours. That's what matters.
        </div>
        <span class="example-tag">Personalization</span>
        <span class="example-tag">All-or-Nothing</span>
      </div>

      <div class="example-card" onclick="loadExample('comparison')">
        <div class="example-thought">"Everyone is better than me"</div>
        <div class="example-response">
          <strong>Reality:</strong> People are different - some are apples, some are oranges, some are peaches. Comparison is pointless when each of us is so different. You have unique strengths and your own path.
        </div>
        <span class="example-tag">Overgeneralization</span>
        <span class="example-tag">Discounting the Positive</span>
      </div>
    </div>
  </div>

  <!-- TAB: TOOLKIT -->
  <div id="tab-toolkit" class="tab-content">
    <div class="card">
      <label class="section-label">Quick Interventions</label>
      <div class="helper-text">Tools to use when feeling overwhelmed</div>

      <div class="toolkit-grid">
        <div class="toolkit-item">
          <div class="toolkit-title">54321 Grounding Technique</div>
          <div class="toolkit-content">
            <ul class="toolkit-steps">
              <li>Name 5 things you can see</li>
              <li>Name 4 things you can touch</li>
              <li>Name 3 things you can hear</li>
              <li>Name 2 things you can smell</li>
              <li>Name 1 thing you can taste</li>
            </ul>
            <em style="color: var(--muted); font-size: 0.875rem;">Brings you back to the present moment</em>
          </div>
        </div>

        <div class="toolkit-item">
          <div class="toolkit-title">Box Breathing</div>
          <div class="toolkit-content">
            <ul class="toolkit-steps">
              <li>Breathe in for 4 counts</li>
              <li>Hold for 4 counts</li>
              <li>Breathe out for 4 counts</li>
              <li>Hold for 4 counts</li>
              <li>Repeat 4-5 times</li>
            </ul>
            <em style="color: var(--muted); font-size: 0.875rem;">Calms the nervous system</em>
          </div>
        </div>

        <div class="toolkit-item">
          <div class="toolkit-title">Fact vs. Thought</div>
          <div class="toolkit-content">
            Ask yourself: "Is this a fact or a thought?"
            <ul class="toolkit-steps">
              <li>Facts: Concrete, observable, provable</li>
              <li>Thoughts: Interpretations, predictions, opinions</li>
              <li>Most distressing things are thoughts, not facts</li>
            </ul>
          </div>
        </div>

        <div class="toolkit-item">
          <div class="toolkit-title">The Friend Test</div>
          <div class="toolkit-content">
            If a friend told you this about themselves, what would you say?
            <ul class="toolkit-steps">
              <li>We're often kinder to friends than ourselves</li>
              <li>This exposes double standards</li>
              <li>Helps find compassionate perspective</li>
            </ul>
          </div>
        </div>

        <div class="toolkit-item">
          <div class="toolkit-title">Break It Down</div>
          <div class="toolkit-content">
            When something feels too hard:
            <ul class="toolkit-steps">
              <li>Put on coat</li>
              <li>Put on shoes</li>
              <li>Go outside</li>
              <li>Walk to the park</li>
              <li>Listen to music</li>
            </ul>
            <em style="color: var(--muted); font-size: 0.875rem;">One tiny step at a time</em>
          </div>
        </div>

        <div class="toolkit-item">
          <div class="toolkit-title">Pain Is Valid</div>
          <div class="toolkit-content">
            Pain can't be measured or compared:
            <ul class="toolkit-steps">
              <li>If it's real to you, it IS real</li>
              <li>Your problems don't take care away from anyone</li>
              <li>You wouldn't tell someone with headaches to "shut up because others have cancer"</li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="saved-msg" id="saved-msg">✓ Record saved successfully</div>

<script>
// ══════════════════════════════════════════════════════════════════════════════
// STARFIELD CANVAS ANIMATION
// ══════════════════════════════════════════════════════════════════════════════
const canvas = document.getElementById('stars-canvas');
const ctx = canvas.getContext('2d');
let stars = [];

function resizeCanvas() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  initStars();
}

function initStars() {
  stars = [];
  const starCount = Math.floor((canvas.width * canvas.height) / 3000);
  for (let i = 0; i < starCount; i++) {
    stars.push({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      radius: Math.random() * 1.5,
      opacity: Math.random() * 0.5 + 0.3,
      twinkleSpeed: Math.random() * 0.02 + 0.005
    });
  }
}

function drawStars() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  stars.forEach(star => {
    star.opacity += star.twinkleSpeed;
    if (star.opacity > 0.8 || star.opacity < 0.2) {
      star.twinkleSpeed = -star.twinkleSpeed;
    }
    ctx.beginPath();
    ctx.arc(star.x, star.y, star.radius, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(240, 232, 208, ${star.opacity})`;
    ctx.fill();
  });
  requestAnimationFrame(drawStars);
}

window.addEventListener('resize', resizeCanvas);
resizeCanvas();
drawStars();

// ══════════════════════════════════════════════════════════════════════════════
// TAB SWITCHING
// ══════════════════════════════════════════════════════════════════════════════
function switchTab(tabName) {
  // Hide all tabs
  document.querySelectorAll('.tab-content').forEach(tab => {
    tab.classList.remove('active');
  });
  
  // Remove active from all nav tabs
  document.querySelectorAll('.nav-tab').forEach(tab => {
    tab.classList.remove('active');
  });
  
  // Show selected tab
  document.getElementById(`tab-${tabName}`).classList.add('active');
  
  // Set active nav tab
  event.target.closest('.nav-tab').classList.add('active');
  
  // Load content if needed
  if (tabName === 'history') {
    renderHistory();
  } else if (tabName === 'insights') {
    renderInsights();
  }
}

// ══════════════════════════════════════════════════════════════════════════════
// INTENSITY SLIDER UPDATE (1-10 scale)
// ══════════════════════════════════════════════════════════════════════════════
const intensitySlider = document.getElementById('intensity');
const intensityValue = document.getElementById('intensity-value');

intensitySlider.addEventListener('input', (e) => {
  intensityValue.textContent = e.target.value;
});

// ══════════════════════════════════════════════════════════════════════════════
// COGNITIVE DISTORTIONS TOGGLE
// ══════════════════════════════════════════════════════════════════════════════
function toggleDistortion(element) {
  element.classList.toggle('selected');
}

function toggleDistortionInfo(trigger) {
  trigger.classList.toggle('expanded');
  const details = document.getElementById('distortion-details');
  details.classList.toggle('expanded');
}

// ══════════════════════════════════════════════════════════════════════════════
// LOAD EXAMPLE INTO FORM
// ══════════════════════════════════════════════════════════════════════════════
const examples = {
  'alone-abroad': {
    thoughts: "I will be all alone abroad. Nobody will care about me when I am abroad.",
    evidenceFor: "",
    evidenceAgainst: "I can't know that for certain. I might find people who will care. It's possible to build new connections.",
    friendResponse: "You can't predict the future with certainty. Many people move abroad and find meaningful connections. It takes time, but it's possible. You have qualities that make you a good friend.",
    conclusion: "It's a thought, not a fact. It's not helpful to assume the worst. I can't know what will happen until I try. The possibility of loneliness doesn't mean it's inevitable.",
    distortions: ['Catastrophizing', 'Fortune Telling']
  },
  'weak': {
    thoughts: "I'm weak",
    evidenceFor: "I cry. I have panic attacks.",
    evidenceAgainst: "I reached out to my friend. I made the decision to go to therapy even though I was terrified. I told my mom about therapy after 8 sessions. I did research on conversion therapy and wrote respectful messages to my professor after she expressed homophobic views. I spent the entire night in a mental breakdown with 9/10 toothache pain, still woke up for an exam in the morning. I studied very hard for my exams without complaining.",
    friendResponse: "You're human, not a robot who can handle everything. You have been very strong, but it hasn't helped you. Softness and vulnerability aren't weaknesses. Those actions you took required immense courage.",
    conclusion: "I am not weak. I'm dealing with difficult circumstances and still showing up. Crying and having panic attacks are human responses to real pain, not signs of weakness.",
    distortions: ['Labeling', 'Discounting the Positive']
  },
  'unintelligent': {
    thoughts: "I'm unintelligent",
    evidenceFor: "I can't come up with creative ideas in class. I can't solve my mental health issues.",
    evidenceAgainst: "200/200 English exam, 200/200 Ukrainian exam, 191/200 History of Ukraine exam. I learned English alone online for a year and got to B2-C1. I started learning French in summer and after a year I am the best at French in my group. I can use AI to create websites for research I did. I started tutoring English in 11th grade, 2+ years of experience, children want to go to me. I created a website for my mom's business.",
    friendResponse: "Mental health issues aren't solved through intelligence alone - they require time, support, and treatment. Your academic achievements and self-teaching abilities clearly demonstrate your intelligence.",
    conclusion: "I have strong evidence of my intelligence through my academic performance and self-directed learning. Mental health struggles don't reflect on intelligence.",
    distortions: ['Labeling', 'All-or-Nothing']
  },
  'uliana-hates': {
    thoughts: "Uliana hates me",
    evidenceFor: "I hurt her by ghosting her for 4 days, then saying our paths have diverged, then apologizing the next day. I made therapy complicated. She didn't say hi and sit next to me today.",
    evidenceAgainst: "She smiled at me in class. She helped me with the exam when she had a fever. She said 'I am not mad at you.' She listened to my apology and wrote a long message back. We talked after class and text each other about normal things. We joked around on our bus ride.",
    friendResponse: "Actions speak louder than one difficult moment. She's continuing to engage with you, help you, and spend time with you. That shows care, not hate. You hurt her, but she's working through it with you.",
    conclusion: "I hurt her because I was hurt too. I handled it poorly but it was the only way I knew. Her current actions show she doesn't hate me - she's processing what happened while still maintaining our friendship.",
    distortions: ['Mind Reading', 'Catastrophizing']
  },
  'nothing-works': {
    thoughts: "No matter how much I try, nothing works",
    evidenceFor: "I still have panic attacks. I still cry. I still have anxiety around people.",
    evidenceAgainst: "I can challenge my thoughts now (progress). I can use techniques: 54321, box breathing, thought/fact testing. I am getting help and I have diagnoses which can take years to treat. I have an easier time talking to people and sharing myself than a year ago.",
    friendResponse: "Recovery isn't linear. The fact that you still have symptoms doesn't mean nothing is working - you're building skills that will compound over time. You're treating clinical disorders that take years, not weeks.",
    conclusion: "Progress is happening even if I can't see it clearly in the moment. I have more tools than I did before. The presence of symptoms doesn't negate the growth.",
    distortions: ['Overgeneralization', 'Discounting the Positive']
  },
  'problems-not-real': {
    thoughts: "My pain isn't real. I don't have any real problems.",
    evidenceFor: "Some people have experienced abuse, financial problems, war, starvation, death of close people.",
    evidenceAgainst: "I have two clinical, diagnosed anxiety disorders: SAD and GAD. I have had 7-8 panic attacks over the past 5 months. I cry often, almost every day, sometimes multiple times. I have been very perfectionistic, self-critical and self-hating. I have had suicidal ideation. I have been feeling lonely, inadequate, worthless, burdensome. I am gay in a homophobic country with a homophobic family.",
    friendResponse: "Pain isn't something that can be measured. If it is real to you and it causes you pain, then it is real. If this isn't real, what is? You wouldn't tell someone with headaches to shut up because others have cancer.",
    conclusion: "Pain can't be compared. My problems don't take care away from anybody. My diagnosed disorders and experiences are valid and deserve treatment.",
    distortions: ['Discounting the Positive', 'Emotional Reasoning']
  },
  'nothing-matters': {
    thoughts: "Nothing I say matters",
    evidenceFor: "They didn't respond to my message about conversion therapy.",
    evidenceAgainst: "The teacher responded, disagreed, but let me post the links. No retaliation, no judgement, no administrative involvement. Some things we say don't register as important to those unaffected by their significance.",
    friendResponse: "Your worth isn't tied to whether they responded, agreed, or ignored your messages. You did the thing you were terrified to do because you couldn't not say anything. That's progress.",
    conclusion: "Not everyone will respond to what matters deeply to me. That doesn't make it meaningless. I expected much worse than what happened. Silence stings, but the silence is theirs, not mine. That's what matters most.",
    distortions: ['Personalization', 'All-or-Nothing']
  },
  'comparison': {
    thoughts: "Everyone is better than me",
    evidenceFor: "People seem more confident, successful, happy.",
    evidenceAgainst: "People are different: some are apples, some are oranges, some are peaches. I have B2-C1 English (self-taught), best at French in my group, 200/200 on multiple exams, created research websites, 2+ years tutoring experience with good reviews.",
    friendResponse: "Comparison is pointless when each of us is so different. You're measuring yourself against a highlight reel. You have unique strengths and your own path.",
    conclusion: "Comparison steals joy and isn't accurate. I have my own strengths and journey. I'm not behind - I'm on my own timeline.",
    distortions: ['Overgeneralization', 'Discounting the Positive']
  }
};

function loadExample(exampleKey) {
  const example = examples[exampleKey];
  if (!example) return;
  
  // Switch to new record tab
  switchTab('new-record');
  
  // Fill form
  document.getElementById('thoughts').value = example.thoughts;
  document.getElementById('evidence-for').value = example.evidenceFor;
  document.getElementById('evidence-against').value = example.evidenceAgainst;
  document.getElementById('friend-response').value = example.friendResponse;
  document.getElementById('conclusion').value = example.conclusion;
  
  // Select distortions
  document.querySelectorAll('.distortion-tag').forEach(tag => {
    tag.classList.remove('selected');
    if (example.distortions.includes(tag.textContent)) {
      tag.classList.add('selected');
    }
  });
  
  // Scroll to top
  window.scrollTo({ top: 0, behavior: 'smooth' });
  
  // Show message
  const msg = document.getElementById('saved-msg');
  msg.textContent = '✓ Example loaded';
  msg.classList.add('show');
  setTimeout(() => {
    msg.classList.remove('show');
    msg.textContent = '✓ Record saved successfully';
  }, 2000);
}

// ══════════════════════════════════════════════════════════════════════════════
// SAVE RECORD
// ══════════════════════════════════════════════════════════════════════════════
function saveRecord() {
  const record = {
    timestamp: new Date().toISOString(),
    situation: document.getElementById('situation').value,
    emotions: document.getElementById('emotions').value,
    intensity: document.getElementById('intensity').value,
    thoughts: document.getElementById('thoughts').value,
    evidenceFor: document.getElementById('evidence-for').value,
    evidenceAgainst: document.getElementById('evidence-against').value,
    distortions: Array.from(document.querySelectorAll('.distortion-tag.selected')).map(el => el.textContent),
    friendResponse: document.getElementById('friend-response').value,
    conclusion: document.getElementById('conclusion').value
  };

  // Save to localStorage
  const savedRecords = JSON.parse(localStorage.getItem('thoughtRecords') || '[]');
  savedRecords.push(record);
  localStorage.setItem('thoughtRecords', JSON.stringify(savedRecords));

  // Show confirmation
  const msg = document.getElementById('saved-msg');
  msg.classList.add('show');
  setTimeout(() => {
    msg.classList.remove('show');
  }, 3000);

  // Optional: clear form after saving
  setTimeout(clearForm, 500);
}

// ══════════════════════════════════════════════════════════════════════════════
// DOWNLOAD CURRENT RECORD AS PDF
// ══════════════════════════════════════════════════════════════════════════════
function downloadCurrentPDF() {
  const record = {
    situation: document.getElementById('situation').value,
    emotions: document.getElementById('emotions').value,
    intensity: document.getElementById('intensity').value,
    thoughts: document.getElementById('thoughts').value,
    evidenceFor: document.getElementById('evidence-for').value,
    evidenceAgainst: document.getElementById('evidence-against').value,
    distortions: Array.from(document.querySelectorAll('.distortion-tag.selected')).map(el => el.textContent),
    friendResponse: document.getElementById('friend-response').value,
    conclusion: document.getElementById('conclusion').value
  };

  generatePDF(record, new Date());
}

// ══════════════════════════════════════════════════════════════════════════════
// GENERATE PDF FROM RECORD
// ══════════════════════════════════════════════════════════════════════════════
function generatePDF(record, date) {
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();
  
  const pageWidth = doc.internal.pageSize.getWidth();
  const margin = 20;
  const maxWidth = pageWidth - 2 * margin;
  let y = 20;
  
  // Title
  doc.setFontSize(20);
  doc.setTextColor(106, 90, 205);
  doc.text('Thought Record', margin, y);
  y += 10;
  
  // Date
  doc.setFontSize(10);
  doc.setTextColor(150, 150, 150);
  doc.text(new Date(date).toLocaleString(), margin, y);
  y += 15;
  
  // Helper function to add section
  const addSection = (label, content) => {
    if (y > 270) {
      doc.addPage();
      y = 20;
    }
    
    doc.setFontSize(12);
    doc.setTextColor(106, 90, 205);
    doc.text(label, margin, y);
    y += 7;
    
    doc.setFontSize(10);
    doc.setTextColor(0, 0, 0);
    if (content) {
      const lines = doc.splitTextToSize(content, maxWidth);
      doc.text(lines, margin, y);
      y += lines.length * 5 + 10;
    } else {
      doc.setTextColor(150, 150, 150);
      doc.text('(not filled)', margin, y);
      y += 12;
    }
  };
  
  // Sections
  addSection('Situation', record.situation);
  addSection('Emotions', record.emotions ? `${record.emotions} (${record.intensity}/10)` : '');
  addSection('Automatic Thoughts', record.thoughts);
  addSection('Evidence For', record.evidenceFor);
  addSection('Evidence Against', record.evidenceAgainst);
  addSection('Cognitive Distortions', record.distortions.join(', '));
  addSection('If a Friend Said This...', record.friendResponse);
  addSection('Balanced Conclusion', record.conclusion);
  
  // Save PDF
  const dateStr = new Date(date).toISOString().split('T')[0];
  doc.save(`thought-record-${dateStr}.pdf`);
}

// ══════════════════════════════════════════════════════════════════════════════
// RENDER SAVED RECORDS
// ══════════════════════════════════════════════════════════════════════════════
function renderHistory() {
  const container = document.getElementById('records-container');
  const savedRecords = JSON.parse(localStorage.getItem('thoughtRecords') || '[]');
  
  if (savedRecords.length === 0) {
    container.innerHTML = '<div class="no-records">No saved records yet</div>';
    return;
  }
  
  // Reverse to show newest first
  container.innerHTML = savedRecords.slice().reverse().map((record, reverseIndex) => {
    const index = savedRecords.length - 1 - reverseIndex; // original index
    const date = new Date(record.timestamp);
    
    return `
      <div class="record-card" id="record-${index}">
        <div class="record-header">
          <div class="record-date">${date.toLocaleDateString()} · ${date.toLocaleTimeString()}</div>
          <div class="record-actions">
            <button class="icon-btn" onclick="editRecord(${index})">
              <svg viewBox="0 0 24 24">
                <path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path>
                <path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path>
              </svg>
              Edit
            </button>
            <button class="icon-btn" onclick="downloadRecordPDF(${index})">
              <svg viewBox="0 0 24 24">
                <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
                <polyline points="14 2 14 8 20 8"></polyline>
                <line x1="16" y1="13" x2="8" y2="13"></line>
                <line x1="16" y1="17" x2="8" y2="17"></line>
                <polyline points="10 9 9 9 8 9"></polyline>
              </svg>
              PDF
            </button>
            <button class="icon-btn icon-btn-delete" onclick="deleteRecord(${index})">
              <svg viewBox="0 0 24 24">
                <polyline points="3 6 5 6 21 6"></polyline>
                <path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path>
              </svg>
              Delete
            </button>
          </div>
        </div>
        <div class="record-content" id="record-content-${index}">
          ${record.situation ? `
            <div class="record-field">
              <div class="record-field-label">Situation</div>
              <div class="record-field-value">${record.situation}</div>
            </div>
          ` : ''}
          ${record.emotions ? `
            <div class="record-field">
              <div class="record-field-label">Emotions (${record.intensity}/10)</div>
              <div class="record-field-value">${record.emotions}</div>
            </div>
          ` : ''}
          ${record.thoughts ? `
            <div class="record-field">
              <div class="record-field-label">Automatic Thoughts</div>
              <div class="record-field-value">${record.thoughts}</div>
            </div>
          ` : ''}
          ${record.evidenceFor || record.evidenceAgainst ? `
            <div class="record-field">
              <div class="record-field-label">Evidence</div>
              <div class="record-field-value">
                ${record.evidenceFor ? `<strong>For:</strong> ${record.evidenceFor}<br>` : ''}
                ${record.evidenceAgainst ? `<strong>Against:</strong> ${record.evidenceAgainst}` : ''}
              </div>
            </div>
          ` : ''}
          ${record.distortions && record.distortions.length > 0 ? `
            <div class="record-field">
              <div class="record-field-label">Cognitive Distortions</div>
              <div class="record-distortions">
                ${record.distortions.map(d => `<span class="record-distortion-tag">${d}</span>`).join('')}
              </div>
            </div>
          ` : ''}
          ${record.friendResponse ? `
            <div class="record-field">
              <div class="record-field-label">If a Friend Said This...</div>
              <div class="record-field-value">${record.friendResponse}</div>
            </div>
          ` : ''}
          ${record.conclusion ? `
            <div class="record-field">
              <div class="record-field-label">Balanced Conclusion</div>
              <div class="record-field-value"><strong>${record.conclusion}</strong></div>
            </div>
          ` : ''}
        </div>
        
        <!-- EDIT FORM (hidden by default) -->
        <div class="edit-form" id="edit-form-${index}">
          <label class="section-label" style="font-size: 1rem;">Edit Record</label>
          <textarea id="edit-situation-${index}" placeholder="Situation">${record.situation || ''}</textarea>
          <textarea id="edit-emotions-${index}" placeholder="Emotions">${record.emotions || ''}</textarea>
          <input type="number" id="edit-intensity-${index}" min="1" max="10" value="${record.intensity || 5}" style="width: 100px; margin-bottom: 0.75rem;">
          <textarea id="edit-thoughts-${index}" placeholder="Automatic Thoughts">${record.thoughts || ''}</textarea>
          <textarea id="edit-evidence-for-${index}" placeholder="Evidence For">${record.evidenceFor || ''}</textarea>
          <textarea id="edit-evidence-against-${index}" placeholder="Evidence Against">${record.evidenceAgainst || ''}</textarea>
          <textarea id="edit-friend-response-${index}" placeholder="If a Friend Said This...">${record.friendResponse || ''}</textarea>
          <textarea id="edit-conclusion-${index}" placeholder="Balanced Conclusion">${record.conclusion || ''}</textarea>
          
          <div class="edit-actions">
            <button class="icon-btn" onclick="saveEdit(${index})" style="background: var(--lavender); color: var(--night);">
              <svg viewBox="0 0 24 24">
                <polyline points="20 6 9 17 4 12"></polyline>
              </svg>
              Save Changes
            </button>
            <button class="icon-btn" onclick="cancelEdit(${index})">
              <svg viewBox="0 0 24 24">
                <line x1="18" y1="6" x2="6" y2="18"></line>
                <line x1="6" y1="6" x2="18" y2="18"></line>
              </svg>
              Cancel
            </button>
          </div>
        </div>
      </div>
    `;
  }).join('');
}

// ══════════════════════════════════════════════════════════════════════════════
// EDIT RECORD
// ══════════════════════════════════════════════════════════════════════════════
function editRecord(index) {
  const recordCard = document.getElementById(`record-${index}`);
  const editForm = document.getElementById(`edit-form-${index}`);
  const recordContent = document.getElementById(`record-content-${index}`);
  
  recordCard.classList.add('edit-mode');
  editForm.classList.add('active');
  recordContent.style.display = 'none';
}

function cancelEdit(index) {
  const recordCard = document.getElementById(`record-${index}`);
  const editForm = document.getElementById(`edit-form-${index}`);
  const recordContent = document.getElementById(`record-content-${index}`);
  
  recordCard.classList.remove('edit-mode');
  editForm.classList.remove('active');
  recordContent.style.display = 'grid';
}

function saveEdit(index) {
  const savedRecords = JSON.parse(localStorage.getItem('thoughtRecords') || '[]');
  
  // Update the record
  savedRecords[index] = {
    ...savedRecords[index],
    situation: document.getElementById(`edit-situation-${index}`).value,
    emotions: document.getElementById(`edit-emotions-${index}`).value,
    intensity: document.getElementById(`edit-intensity-${index}`).value,
    thoughts: document.getElementById(`edit-thoughts-${index}`).value,
    evidenceFor: document.getElementById(`edit-evidence-for-${index}`).value,
    evidenceAgainst: document.getElementById(`edit-evidence-against-${index}`).value,
    friendResponse: document.getElementById(`edit-friend-response-${index}`).value,
    conclusion: document.getElementById(`edit-conclusion-${index}`).value
  };
  
  localStorage.setItem('thoughtRecords', JSON.stringify(savedRecords));
  
  // Show confirmation
  const msg = document.getElementById('saved-msg');
  msg.textContent = '✓ Changes saved successfully';
  msg.classList.add('show');
  setTimeout(() => {
    msg.classList.remove('show');
    msg.textContent = '✓ Record saved successfully';
  }, 3000);
  
  // Re-render history
  renderHistory();
}

// ══════════════════════════════════════════════════════════════════════════════
// DOWNLOAD SAVED RECORD AS PDF
// ══════════════════════════════════════════════════════════════════════════════
function downloadRecordPDF(index) {
  const savedRecords = JSON.parse(localStorage.getItem('thoughtRecords') || '[]');
  const record = savedRecords[index];
  if (record) {
    generatePDF(record, record.timestamp);
  }
}

// ══════════════════════════════════════════════════════════════════════════════
// DELETE RECORD
// ══════════════════════════════════════════════════════════════════════════════
function deleteRecord(index) {
  if (!confirm('Are you sure you want to delete this record?')) return;
  
  const savedRecords = JSON.parse(localStorage.getItem('thoughtRecords') || '[]');
  savedRecords.splice(index, 1);
  localStorage.setItem('thoughtRecords', JSON.stringify(savedRecords));
  
  renderHistory();
  renderInsights(); // Update insights after deletion
}

// ══════════════════════════════════════════════════════════════════════════════
// INSIGHTS & ANALYTICS
// ══════════════════════════════════════════════════════════════════════════════
let intensityChart = null;

function renderInsights() {
  const savedRecords = JSON.parse(localStorage.getItem('thoughtRecords') || '[]');
  
  if (savedRecords.length === 0) {
    document.getElementById('total-records').textContent = '0';
    document.getElementById('avg-intensity').textContent = '-';
    document.getElementById('last-week').textContent = '0';
    document.getElementById('pattern-list').innerHTML = '<div class="no-records">No data yet</div>';
    return;
  }
  
  // Calculate stats
  const totalRecords = savedRecords.length;
  const intensities = savedRecords.map(r => parseInt(r.intensity) || 5);
  const avgIntensity = (intensities.reduce((a, b) => a + b, 0) / intensities.length).toFixed(1);
  
  // Last week count
  const weekAgo = new Date();
  weekAgo.setDate(weekAgo.getDate() - 7);
  const lastWeekCount = savedRecords.filter(r => new Date(r.timestamp) > weekAgo).length;
  
  document.getElementById('total-records').textContent = totalRecords;
  document.getElementById('avg-intensity').textContent = avgIntensity;
  document.getElementById('last-week').textContent = lastWeekCount;
  
  // Render chart
  renderIntensityChart(savedRecords);
  
  // Render patterns
  renderPatterns(savedRecords);
}

function renderIntensityChart(records) {
  const ctx = document.getElementById('intensityChart');
  if (!ctx) return;
  
  // Destroy existing chart
  if (intensityChart) {
    intensityChart.destroy();
  }
  
  // Prepare data (last 10 records)
  const recentRecords = records.slice(-10);
  const labels = recentRecords.map((r, i) => `Record ${records.length - 10 + i + 1}`);
  const data = recentRecords.map(r => parseInt(r.intensity) || 5);
  
  intensityChart = new Chart(ctx, {
    type: 'line',
    data: {
      labels: labels,
      datasets: [{
        label: 'Emotional Intensity',
        data: data,
        borderColor: '#c9b8e8',
        backgroundColor: 'rgba(201, 184, 232, 0.1)',
        tension: 0.4,
        fill: true
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: {
          display: false
        }
      },
      scales: {
        y: {
          beginAtZero: false,
          min: 1,
          max: 10,
          ticks: {
            color: '#e8e0f0',
            stepSize: 1
          },
          grid: {
            color: 'rgba(255, 255, 255, 0.08)'
          }
        },
        x: {
          ticks: {
            color: '#e8e0f0'
          },
          grid: {
            color: 'rgba(255, 255, 255, 0.08)'
          }
        }
      }
    }
  });
}

function renderPatterns(records) {
  const container = document.getElementById('pattern-list');
  
  // Count distortions
  const distortionCounts = {};
  records.forEach(record => {
    if (record.distortions && Array.isArray(record.distortions)) {
      record.distortions.forEach(d => {
        distortionCounts[d] = (distortionCounts[d] || 0) + 1;
      });
    }
  });
  
  // Sort by count
  const sorted = Object.entries(distortionCounts)
    .sort((a, b) => b[1] - a[1])
    .slice(0, 5);
  
  if (sorted.length === 0) {
    container.innerHTML = '<div class="no-records">No patterns identified yet</div>';
    return;
  }
  
  container.innerHTML = sorted.map(([name, count]) => `
    <div class="pattern-item">
      <div class="pattern-name">${name}</div>
      <div class="pattern-count">${count}</div>
    </div>
  `).join('');
}

// ══════════════════════════════════════════════════════════════════════════════
// CLEAR FORM
// ══════════════════════════════════════════════════════════════════════════════
function clearForm() {
  document.getElementById('situation').value = '';
  document.getElementById('emotions').value = '';
  document.getElementById('intensity').value = 5;
  document.getElementById('intensity-value').textContent = 5;
  document.getElementById('thoughts').value = '';
  document.getElementById('evidence-for').value = '';
  document.getElementById('evidence-against').value = '';
  document.getElementById('friend-response').value = '';
  document.getElementById('conclusion').value = '';
  
  // Deselect all distortions
  document.querySelectorAll('.distortion-tag.selected').forEach(tag => {
    tag.classList.remove('selected');
  });
}
</script>

</body>
</html>
