<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Thought Record · CBT Worksheet</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300;1,400&family=DM+Sans:wght@300;400;500&family=Allura&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
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

.subtitle {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.1rem;
  color: var(--muted);
  font-style: italic;
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
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.3rem;
  color: var(--lavender);
  margin-bottom: 0.75rem;
  display: block;
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
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.1rem;
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
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.btn-primary {
  background: linear-gradient(135deg, var(--lavender) 0%, var(--blush) 100%);
  color: var(--night);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(201,184,232,0.3);
}

.btn-secondary {
  background: rgba(255,255,255,0.05);
  border: 1px solid var(--card-border);
  color: var(--text);
}

.btn-secondary:hover {
  background: rgba(255,255,255,0.08);
}

/* ── SAVED MESSAGE ── */
.saved-msg {
  position: fixed;
  top: 2rem;
  right: 2rem;
  background: linear-gradient(135deg, var(--lavender) 0%, var(--blush) 100%);
  color: var(--night);
  padding: 1rem 1.5rem;
  border-radius: 12px;
  font-weight: 500;
  opacity: 0;
  transform: translateY(-20px);
  transition: all 0.3s ease;
  z-index: 1000;
  pointer-events: none;
}

.saved-msg.show {
  opacity: 1;
  transform: translateY(0);
}

/* ── SAVED RECORDS HISTORY ── */
.history-section {
  margin-top: 3rem;
}

.history-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
}

.history-title {
  font-family: 'Allura', cursive;
  font-size: 2rem;
  color: var(--moon);
}

.record-card {
  background: var(--card);
  border: 1px solid var(--card-border);
  border-radius: var(--radius);
  padding: 1.5rem;
  backdrop-filter: blur(20px);
  margin-bottom: 1rem;
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
  color: var(--lavender);
  font-size: 1.1rem;
}

.record-actions {
  display: flex;
  gap: 0.5rem;
}

.btn-small {
  padding: 0.5rem 1rem;
  border-radius: 8px;
  border: none;
  font-family: 'DM Sans', sans-serif;
  font-size: 0.875rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-download {
  background: rgba(212,169,106,0.2);
  border: 1px solid var(--gold);
  color: var(--gold);
}

.btn-download:hover {
  background: rgba(212,169,106,0.3);
}

.btn-delete {
  background: rgba(232,200,212,0.1);
  border: 1px solid rgba(232,200,212,0.3);
  color: var(--blush);
}

.btn-delete:hover {
  background: rgba(232,200,212,0.2);
}

.record-content {
  display: grid;
  gap: 1rem;
}

.record-field {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.record-field-label {
  font-size: 0.875rem;
  color: var(--muted);
  font-weight: 500;
}

.record-field-value {
  color: var(--text);
  line-height: 1.6;
}

.record-distortions {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.record-distortion-tag {
  background: rgba(201,184,232,0.15);
  border: 1px solid rgba(201,184,232,0.3);
  color: var(--lavender);
  padding: 0.25rem 0.75rem;
  border-radius: 12px;
  font-size: 0.8rem;
}

.no-records {
  text-align: center;
  padding: 3rem;
  color: var(--muted);
  font-style: italic;
}
</style>
</head>
<body>

<!-- Animated starfield background -->
<canvas id="stars-canvas"></canvas>

<div class="container">
  <!-- Header -->
  <div class="header">
    <h1 class="title">Thought Record</h1>
    <p class="subtitle">Socratic Questioning · CBT Worksheet</p>
  </div>

  <!-- Main Card -->
  <div class="card">
    <!-- Situation -->
    <div class="section">
      <label class="section-label">Situation</label>
      <p class="helper-text">What happened? Where were you? Who was involved?</p>
      <textarea id="situation" placeholder="Describe the situation objectively..."></textarea>
    </div>

    <!-- Emotions + Intensity -->
    <div class="section">
      <label class="section-label">Emotions</label>
      <p class="helper-text">What did you feel? How intense was it?</p>
      <div class="emotion-row">
        <div>
          <input type="text" id="emotions" placeholder="e.g., anxious, sad, angry, ashamed">
        </div>
        <div>
          <label class="intensity-label">Intensity</label>
          <input type="range" id="intensity" min="0" max="100" value="50">
          <div class="intensity-value"><span id="intensity-value">50</span>%</div>
        </div>
      </div>
    </div>

    <!-- Automatic Thoughts -->
    <div class="section">
      <label class="section-label">Automatic Thoughts</label>
      <p class="helper-text">What went through your mind? What does this mean about you?</p>
      <textarea id="thoughts" placeholder="Write down the thoughts that came up..."></textarea>
    </div>

    <!-- Evidence Grid -->
    <div class="evidence-grid">
      <!-- Evidence FOR -->
      <div class="evidence-box for">
        <div class="evidence-title">Evidence For</div>
        <p class="helper-text">What facts support this thought?</p>
        <textarea id="evidence-for" placeholder="List objective facts..."></textarea>
      </div>

      <!-- Evidence AGAINST -->
      <div class="evidence-box against">
        <div class="evidence-title">Evidence Against</div>
        <p class="helper-text">What facts contradict this thought?</p>
        <textarea id="evidence-against" placeholder="List objective facts..."></textarea>
      </div>
    </div>

    <!-- Cognitive Distortions -->
    <div class="section">
      <label class="section-label">Cognitive Distortions</label>
      <p class="helper-text">Which thinking traps might be active?</p>
      <div class="distortion-tags">
        <div class="distortion-tag" onclick="toggleDistortion(this)">All-or-Nothing</div>
        <div class="distortion-tag" onclick="toggleDistortion(this)">Overgeneralization</div>
        <div class="distortion-tag" onclick="toggleDistortion(this)">Mental Filter</div>
        <div class="distortion-tag" onclick="toggleDistortion(this)">Discounting Positives</div>
        <div class="distortion-tag" onclick="toggleDistortion(this)">Jumping to Conclusions</div>
        <div class="distortion-tag" onclick="toggleDistortion(this)">Magnification</div>
        <div class="distortion-tag" onclick="toggleDistortion(this)">Emotional Reasoning</div>
        <div class="distortion-tag" onclick="toggleDistortion(this)">Should Statements</div>
        <div class="distortion-tag" onclick="toggleDistortion(this)">Labeling</div>
        <div class="distortion-tag" onclick="toggleDistortion(this)">Personalization</div>
      </div>
    </div>

    <!-- If a Friend Said This -->
    <div class="section">
      <label class="section-label">If a Friend Said This...</label>
      <p class="helper-text">What would you tell a friend who had this thought?</p>
      <textarea id="friend-response" placeholder="Write with compassion..."></textarea>
    </div>

    <!-- Balanced Conclusion -->
    <div class="section">
      <label class="section-label">The Most Balanced Conclusion</label>
      <p class="helper-text">Considering all the evidence, what's a more balanced way to think about this?</p>
      <div class="conclusion-box">
        <textarea id="conclusion" placeholder="Write a balanced, compassionate alternative thought..."></textarea>
      </div>
    </div>

    <!-- Actions -->
    <div class="actions">
      <button class="btn btn-secondary" onclick="clearForm()">
        <span>✨</span> Clear
      </button>
      <button class="btn btn-secondary" onclick="downloadCurrentPDF()">
        <span>📄</span> Download PDF
      </button>
      <button class="btn btn-primary" onclick="saveRecord()">
        <span>💫</span> Save Record
      </button>
    </div>
  </div>

  <!-- Saved Records History -->
  <div class="history-section" id="history-section" style="display: none;">
    <div class="history-header">
      <h2 class="history-title">Saved Records</h2>
      <button class="btn btn-secondary btn-small" onclick="toggleHistory()">
        <span>✕</span> Close
      </button>
    </div>
    <div id="records-container"></div>
  </div>

  <!-- View History Button (fixed at bottom) -->
  <div style="text-align: center; margin-top: 2rem;">
    <button class="btn btn-secondary" onclick="toggleHistory()" id="view-history-btn">
      <span>📚</span> View Saved Records
    </button>
  </div>
</div>

<!-- Saved confirmation message -->
<div class="saved-msg" id="saved-msg">
  ✓ Thought record saved
</div>

<script>
// ══════════════════════════════════════════════════════════════════════════════
// ANIMATED STARFIELD BACKGROUND
// ══════════════════════════════════════════════════════════════════════════════
const canvas = document.getElementById('stars-canvas');
const ctx = canvas.getContext('2d');

function resizeCanvas() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
}
resizeCanvas();
window.addEventListener('resize', resizeCanvas);

// Create stars
const stars = [];
for (let i = 0; i < 100; i++) {
  stars.push({
    x: Math.random() * canvas.width,
    y: Math.random() * canvas.height,
    radius: Math.random() * 1.5,
    opacity: Math.random(),
    twinkleSpeed: Math.random() * 0.02 + 0.01
  });
}

function animateStars() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  
  stars.forEach(star => {
    star.opacity += star.twinkleSpeed;
    if (star.opacity > 1 || star.opacity < 0) {
      star.twinkleSpeed *= -1;
    }
    
    ctx.beginPath();
    ctx.arc(star.x, star.y, star.radius, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(201, 184, 232, ${star.opacity * 0.6})`;
    ctx.fill();
  });
  
  requestAnimationFrame(animateStars);
}
animateStars();

// ══════════════════════════════════════════════════════════════════════════════
// INTENSITY SLIDER UPDATE
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
  addSection('Emotions', record.emotions ? `${record.emotions} (${record.intensity}%)` : '');
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
// TOGGLE HISTORY VIEW
// ══════════════════════════════════════════════════════════════════════════════
function toggleHistory() {
  const historySection = document.getElementById('history-section');
  const viewBtn = document.getElementById('view-history-btn');
  
  if (historySection.style.display === 'none') {
    historySection.style.display = 'block';
    viewBtn.style.display = 'none';
    renderHistory();
  } else {
    historySection.style.display = 'none';
    viewBtn.style.display = 'inline-flex';
  }
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
  container.innerHTML = savedRecords.reverse().map((record, reverseIndex) => {
    const index = savedRecords.length - 1 - reverseIndex; // original index
    const date = new Date(record.timestamp);
    
    return `
      <div class="record-card">
        <div class="record-header">
          <div class="record-date">${date.toLocaleDateString()} · ${date.toLocaleTimeString()}</div>
          <div class="record-actions">
            <button class="btn-small btn-download" onclick="downloadRecordPDF(${index})">
              📄 PDF
            </button>
            <button class="btn-small btn-delete" onclick="deleteRecord(${index})">
              🗑️ Delete
            </button>
          </div>
        </div>
        <div class="record-content">
          ${record.situation ? `
            <div class="record-field">
              <div class="record-field-label">Situation</div>
              <div class="record-field-value">${record.situation}</div>
            </div>
          ` : ''}
          ${record.emotions ? `
            <div class="record-field">
              <div class="record-field-label">Emotions (${record.intensity}%)</div>
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
      </div>
    `;
  }).join('');
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
}

// ══════════════════════════════════════════════════════════════════════════════
// CLEAR FORM
// ══════════════════════════════════════════════════════════════════════════════
function clearForm() {
  document.getElementById('situation').value = '';
  document.getElementById('emotions').value = '';
  document.getElementById('intensity').value = 50;
  document.getElementById('intensity-value').textContent = 50;
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
