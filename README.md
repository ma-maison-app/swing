<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Swing · A Gentle Diary</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300;1,400&family=DM+Sans:wght@300;400&family=Allura&display=swap" rel="stylesheet">
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
  padding-bottom: 80px;
}

/* ── CANVAS STARFIELD ── */
#stars-canvas {
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100%;
  pointer-events: none;
  z-index: 0;
}

/* ── MOBILE LAYOUT ── */
.shell {
  position: relative;
  z-index: 1;
  min-height: 100vh;
}

/* ── MOBILE HEADER ── */
.mobile-header {
  position: sticky;
  top: 0;
  z-index: 100;
  background: rgba(13,17,36,0.95);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--card-border);
  padding: 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.header-logo {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.app-name {
  font-family: 'Allura', cursive;
  font-size: 1.5rem;
  color: var(--moon);
  line-height: 1;
}

.menu-btn {
  background: none;
  border: none;
  color: var(--lavender);
  font-size: 1.5rem;
  cursor: pointer;
  padding: 0.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* ── SOUND BUTTON ── */
.sound-btn {
  background: none;
  border: none;
  color: var(--muted);
  cursor: pointer;
  padding: 0.5rem;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
  opacity: 0.6;
}

.sound-btn:hover {
  color: var(--lavender);
  opacity: 1;
}

.sound-btn.playing {
  color: var(--lavender);
  opacity: 1;
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.6; }
}

/* ── SOUND MENU POPUP ── */
.sound-menu {
  position: fixed;
  top: 70px;
  right: 1rem;
  width: 280px;
  max-height: 80vh;
  background: rgba(13,17,36,0.98);
  backdrop-filter: blur(20px);
  border: 1px solid var(--card-border);
  border-radius: var(--radius);
  z-index: 150;
  opacity: 0;
  pointer-events: none;
  transform: translateY(-10px);
  transition: all 0.3s ease;
  overflow: hidden;
}

.sound-menu.open {
  opacity: 1;
  pointer-events: auto;
  transform: translateY(0);
}

.sound-menu-header {
  padding: 1rem 1.25rem;
  border-bottom: 1px solid var(--card-border);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.sound-menu-header h3 {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.1rem;
  font-weight: 400;
  color: var(--lavender);
  margin: 0;
}

.sound-close {
  background: none;
  border: none;
  color: var(--muted);
  cursor: pointer;
  padding: 0.25rem;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
}

.sound-close:hover {
  color: var(--lavender);
}

.sound-tracks {
  max-height: 300px;
  overflow-y: auto;
  padding: 0.5rem;
}

.sound-track {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s ease;
  color: var(--muted);
  margin-bottom: 2px;
}

.sound-track:hover {
  background: rgba(255,255,255,0.04);
  color: var(--text);
}

.sound-track.active {
  background: rgba(201,184,232,0.12);
  color: var(--lavender);
}

.sound-track svg {
  flex-shrink: 0;
}

.sound-track span {
  font-size: 0.85rem;
}

.sound-controls {
  padding: 1rem 1.25rem;
  border-top: 1px solid var(--card-border);
  display: flex;
  align-items: center;
  gap: 1rem;
}

.sound-play-btn {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background: rgba(201,184,232,0.12);
  border: 1px solid var(--lavender);
  color: var(--lavender);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
  flex-shrink: 0;
  padding: 0;
}

.sound-play-btn:hover {
  background: rgba(201,184,232,0.2);
  transform: scale(1.05);
}

.sound-volume {
  flex: 1;
  height: 4px;
  border-radius: 2px;
  background: var(--card-border);
  outline: none;
  -webkit-appearance: none;
}

.sound-volume::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: var(--lavender);
  cursor: pointer;
}

.sound-volume::-moz-range-thumb {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: var(--lavender);
  cursor: pointer;
  border: none;
}

/* ── MOBILE NAV DRAWER ── */
.nav-drawer {
  position: fixed;
  top: 0;
  left: -100%;
  width: 80%;
  max-width: 280px;
  height: 100vh;
  background: rgba(13,17,36,0.98);
  backdrop-filter: blur(20px);
  border-right: 1px solid var(--card-border);
  z-index: 200;
  transition: left 0.3s ease;
  overflow-y: auto;
  padding: 2rem 0;
}

.nav-drawer.open {
  left: 0;
}

.nav-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.6);
  z-index: 199;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
}

.nav-overlay.show {
  opacity: 1;
  pointer-events: auto;
}

.nav-drawer-header {
  padding: 0 1.5rem 2rem;
  border-bottom: 1px solid var(--card-border);
  margin-bottom: 1.5rem;
}

.nav-drawer .app-name {
  font-size: 2rem;
}

.nav-drawer .app-tagline {
  font-size: 0.7rem;
  color: var(--muted);
  letter-spacing: 0.15em;
  text-transform: uppercase;
  margin-top: 0.3rem;
}

.nav-section {
  padding: 0 1rem;
  margin-bottom: 0.5rem;
}

.nav-label {
  font-size: 0.6rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--muted);
  padding: 0 0.5rem;
  margin-bottom: 0.5rem;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.65rem 0.75rem;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.2s ease;
  font-size: 0.85rem;
  color: var(--muted);
  border: 1px solid transparent;
  margin-bottom: 2px;
}

.nav-item:hover {
  background: var(--card);
  color: var(--text);
}

.nav-item.active {
  background: rgba(201,184,232,0.12);
  border-color: rgba(201,184,232,0.2);
  color: var(--lavender);
}

.nav-icon { 
  font-size: 1rem; 
  width: 20px; 
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* ── MAIN CONTENT ── */
.main {
  padding: 1.5rem 1rem;
  max-width: 600px;
  margin: 0 auto;
}

/* ── SCREENS ── */
.screen { display: none; }
.screen.active { display: block; }

/* ── PAGE HEADER ── */
.page-header {
  margin-bottom: 2rem;
}

.page-title {
  font-family: 'Cormorant Garamond', serif;
  font-size: 2rem;
  font-weight: 300;
  color: var(--moon);
  line-height: 1.1;
}

.page-subtitle {
  font-size: 0.85rem;
  color: var(--muted);
  margin-top: 0.4rem;
  font-style: italic;
  font-family: 'Cormorant Garamond', serif;
}

/* ── CARDS ── */
.card {
  background: var(--card);
  border: 1px solid var(--card-border);
  border-radius: var(--radius);
  padding: 1.5rem;
  backdrop-filter: blur(10px);
  margin-bottom: 1rem;
  transition: border-color 0.3s ease;
}

.card:hover { border-color: rgba(201,184,232,0.2); }

.card-title {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.1rem;
  font-weight: 400;
  color: var(--lavender);
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

/* ── FORM ELEMENTS ── */
label {
  display: block;
  font-size: 0.75rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--muted);
  margin-bottom: 0.5rem;
  margin-top: 1rem;
}

label:first-child { margin-top: 0; }

input[type="text"],
input[type="number"],
textarea,
select {
  width: 100%;
  background: rgba(255,255,255,0.04);
  border: 1px solid var(--card-border);
  border-radius: 10px;
  padding: 0.75rem 1rem;
  color: var(--text);
  font-family: 'DM Sans', sans-serif;
  font-size: 0.9rem;
  outline: none;
  transition: border-color 0.2s;
  resize: vertical;
}

input:focus, textarea:focus, select:focus {
  border-color: rgba(201,184,232,0.4);
}

select option { background: var(--deep); }

textarea { min-height: 80px; line-height: 1.6; }

.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  border-radius: 10px;
  border: 1px solid var(--card-border);
  background: rgba(201,184,232,0.1);
  color: var(--lavender);
  font-family: 'DM Sans', sans-serif;
  font-size: 0.85rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.btn:hover {
  background: rgba(201,184,232,0.15);
  border-color: rgba(201,184,232,0.3);
}

.btn-primary {
  background: linear-gradient(135deg, rgba(201,184,232,0.2), rgba(232,200,212,0.15));
  border-color: var(--lavender);
}

.btn-primary:hover {
  background: linear-gradient(135deg, rgba(201,184,232,0.3), rgba(232,200,212,0.25));
}

/* ── HOME SCREEN ── */
.home-grid {
  display: grid;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.home-tile {
  background: var(--card);
  border: 1px solid var(--card-border);
  border-radius: var(--radius);
  padding: 1.25rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.home-tile:hover { border-color: rgba(201,184,232,0.2); }

.tile-label {
  font-size: 0.7rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--muted);
  margin-bottom: 0.5rem;
}

.tile-content {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.5rem;
  color: var(--moon);
}

.tile-icon {
  font-size: 1.5rem;
  margin-right: 0.5rem;
}

/* ── EMOTION TAGS (EXPANDED) ── */
.emotion-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.emotion-tag {
  padding: 0.5rem 1rem;
  border-radius: 20px;
  background: rgba(255,255,255,0.04);
  border: 1px solid var(--card-border);
  color: var(--muted);
  font-size: 0.8rem;
  cursor: pointer;
  transition: all 0.2s ease;
  user-select: none;
}

.emotion-tag:hover {
  border-color: rgba(201,184,232,0.3);
  background: rgba(201,184,232,0.08);
}

.emotion-tag.selected {
  background: rgba(201,184,232,0.15);
  border-color: var(--lavender);
  color: var(--lavender);
}

/* ── SELF-COMPASSION EXERCISES ── */
.compassion-prompt {
  background: rgba(201,184,232,0.06);
  border-left: 3px solid var(--lavender);
  padding: 1rem;
  border-radius: 8px;
  margin-bottom: 1rem;
  font-style: italic;
  color: var(--text);
  line-height: 1.6;
}

.prompt-category {
  font-size: 0.65rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--lavender);
  margin-bottom: 0.5rem;
}

/* ── WIN OF THE DAY ── */
.win-input-section {
  margin-bottom: 2rem;
}

.win-list {
  margin-top: 1.5rem;
}

.win-entry {
  background: var(--card);
  border: 1px solid var(--card-border);
  border-radius: 12px;
  padding: 1rem;
  margin-bottom: 0.75rem;
  display: flex;
  align-items: flex-start;
  gap: 1rem;
}

.win-date {
  font-size: 0.7rem;
  color: var(--muted);
  text-align: center;
  min-width: 50px;
}

.win-day {
  font-size: 1.3rem;
  color: var(--gold);
  font-weight: 500;
}

.win-month {
  font-size: 0.6rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}

.win-content {
  flex: 1;
  line-height: 1.5;
  color: var(--text);
}

.win-icon {
  font-size: 1.2rem;
  margin-right: 0.5rem;
}

/* ── MOOD CALENDAR/GRAPH ── */
.mood-calendar {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 0.5rem;
  margin-top: 1rem;
}

.mood-day {
  aspect-ratio: 1;
  border-radius: 8px;
  background: var(--card);
  border: 1px solid var(--card-border);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: 0.7rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.mood-day:hover {
  border-color: rgba(201,184,232,0.3);
}

.mood-day.has-mood {
  border-width: 2px;
}

.mood-day.mood-great {
  background: rgba(106, 212, 148, 0.15);
  border-color: rgba(106, 212, 148, 0.5);
}

.mood-day.mood-good {
  background: rgba(201, 184, 232, 0.15);
  border-color: rgba(201, 184, 232, 0.5);
}

.mood-day.mood-okay {
  background: rgba(212, 169, 106, 0.15);
  border-color: rgba(212, 169, 106, 0.5);
}

.mood-day.mood-low {
  background: rgba(232, 152, 152, 0.15);
  border-color: rgba(232, 152, 152, 0.5);
}

.mood-day.mood-struggling {
  background: rgba(139, 92, 246, 0.15);
  border-color: rgba(139, 92, 246, 0.5);
}

.day-number {
  font-size: 0.75rem;
  color: var(--muted);
  margin-bottom: 2px;
}

.day-emoji {
  font-size: 1.1rem;
}

.calendar-header {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 0.5rem;
  margin-bottom: 0.5rem;
  text-align: center;
  font-size: 0.65rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--muted);
}

.mood-legend {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin-top: 1.5rem;
  padding-top: 1.5rem;
  border-top: 1px solid var(--card-border);
}

.legend-item {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  font-size: 0.75rem;
  color: var(--muted);
}

.legend-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  border: 2px solid;
}

/* ── MUSIC PLAYER ── */
.music-player {
  background: var(--card);
  border: 1px solid var(--card-border);
  border-radius: var(--radius);
  padding: 1.5rem;
  margin-bottom: 1.5rem;
}

.player-controls {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1rem;
}

.play-btn {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: rgba(201,184,232,0.15);
  border: 1px solid var(--lavender);
  color: var(--lavender);
  font-size: 1.2rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease;
}

.play-btn:hover {
  background: rgba(201,184,232,0.25);
  transform: scale(1.05);
}

.track-info {
  flex: 1;
}

.track-title {
  font-size: 0.9rem;
  color: var(--text);
  margin-bottom: 0.25rem;
}

.track-duration {
  font-size: 0.7rem;
  color: var(--muted);
}

.playlist {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.playlist-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.75rem;
  background: rgba(255,255,255,0.02);
  border: 1px solid var(--card-border);
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.playlist-item:hover {
  background: rgba(201,184,232,0.08);
  border-color: rgba(201,184,232,0.2);
}

.playlist-item.active {
  background: rgba(201,184,232,0.12);
  border-color: var(--lavender);
}

.track-name {
  font-size: 0.85rem;
  color: var(--text);
}

.volume-control {
  margin-top: 1rem;
  display: flex;
  align-items: center;
  gap: 1rem;
}

.volume-slider {
  flex: 1;
  height: 4px;
  border-radius: 2px;
  background: var(--card-border);
  outline: none;
  -webkit-appearance: none;
}

.volume-slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: var(--lavender);
  cursor: pointer;
}

.volume-slider::-moz-range-thumb {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: var(--lavender);
  cursor: pointer;
  border: none;
}

/* ── THOUGHT RECORD CARDS ── */
.thought-card {
  background: var(--card);
  border: 1px solid var(--card-border);
  border-radius: var(--radius);
  padding: 1.25rem;
  margin-bottom: 1rem;
}

.thought-section {
  margin-bottom: 1rem;
}

.thought-section:last-child {
  margin-bottom: 0;
}

.section-label {
  font-size: 0.7rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--lavender);
  margin-bottom: 0.5rem;
}

.thought-text {
  color: var(--text);
  line-height: 1.6;
  font-size: 0.9rem;
}

/* ── HABIT TRACKING ── */
.water-bubbles {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
  margin-top: 1rem;
}

.bubble {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: rgba(255,255,255,0.04);
  border: 2px solid var(--card-border);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  cursor: pointer;
  transition: all 0.2s ease;
  opacity: 0.3;
}

.bubble:hover {
  border-color: rgba(201,184,232,0.3);
  transform: scale(1.1);
}

.bubble.filled {
  opacity: 1;
  border-color: rgba(106, 212, 212, 0.6);
  background: rgba(106, 212, 212, 0.1);
}

.mood-dots {
  display: flex;
  gap: 0.75rem;
  margin-top: 1rem;
}

.mood-dot {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: rgba(255,255,255,0.04);
  border: 2px solid var(--card-border);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.mood-dot:hover {
  border-color: rgba(201,184,232,0.3);
  transform: scale(1.1);
}

.mood-dot.selected {
  border-color: var(--lavender);
  background: rgba(201,184,232,0.1);
  transform: scale(1.15);
}

/* ── BREATHING ── */
.breath-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem 1rem;
}

.breath-orb {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(201,184,232,0.3), rgba(201,184,232,0.05));
  border: 2px solid var(--lavender);
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 2rem 0;
  transition: all 0.3s ease;
  position: relative;
}

.breath-label {
  font-size: 3rem;
  color: var(--lavender);
  position: absolute;
}

.breath-count {
  position: absolute;
  bottom: 30px;
  font-size: 1.5rem;
  color: var(--muted);
}

.breath-orb.inhale {
  transform: scale(1.3);
  background: radial-gradient(circle, rgba(201,184,232,0.4), rgba(201,184,232,0.1));
}

.breath-orb.exhale {
  transform: scale(0.7);
  background: radial-gradient(circle, rgba(201,184,232,0.2), rgba(201,184,232,0.02));
}

.breath-orb.hold {
  transform: scale(1.3);
  background: radial-gradient(circle, rgba(212,169,106,0.3), rgba(212,169,106,0.05));
}

.breath-instruction {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.5rem;
  color: var(--text);
  margin-bottom: 2rem;
}

.pattern-selector {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
}

.pattern-btn {
  padding: 0.5rem 1rem;
  border-radius: 20px;
  background: rgba(255,255,255,0.04);
  border: 1px solid var(--card-border);
  color: var(--muted);
  font-size: 0.8rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.pattern-btn:hover {
  border-color: rgba(201,184,232,0.3);
  background: rgba(201,184,232,0.08);
}

.pattern-btn.active {
  background: rgba(201,184,232,0.15);
  border-color: var(--lavender);
  color: var(--lavender);
}

/* ── BEHAVIORAL ACTIVATION ── */
.action-step-row {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 0.75rem;
}

.step-check {
  width: 24px;
  height: 24px;
  border-radius: 6px;
  border: 2px solid var(--card-border);
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.2s ease;
  color: transparent;
  font-size: 0.9rem;
}

.step-check:hover {
  border-color: rgba(201,184,232,0.3);
}

.step-check.done {
  background: rgba(106, 212, 148, 0.15);
  border-color: rgba(106, 212, 148, 0.6);
  color: rgba(106, 212, 148, 1);
}

.action-step-row input {
  flex: 1;
}

/* ── ENTRIES ── */
.entry-card {
  background: var(--card);
  border: 1px solid var(--card-border);
  border-radius: var(--radius);
  padding: 1.25rem;
  margin-bottom: 1rem;
  display: flex;
  gap: 1rem;
  cursor: pointer;
  transition: all 0.2s ease;
}

.entry-card:hover {
  border-color: rgba(201,184,232,0.2);
}

.entry-date-block {
  text-align: center;
  min-width: 50px;
}

.entry-day {
  font-size: 1.5rem;
  font-weight: 500;
  color: var(--gold);
  line-height: 1;
}

.entry-month {
  font-size: 0.6rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--muted);
  margin-top: 0.25rem;
}

.entry-body {
  flex: 1;
}

.entry-title {
  font-family: 'Cormorant Garamond', serif;
  font-size: 1.1rem;
  color: var(--moon);
  margin-bottom: 0.5rem;
}

.entry-preview {
  font-size: 0.85rem;
  color: var(--muted);
  line-height: 1.5;
  margin-bottom: 0.75rem;
}

.entry-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
}

.entry-tag {
  padding: 0.25rem 0.6rem;
  border-radius: 12px;
  background: rgba(201,184,232,0.1);
  border: 1px solid rgba(201,184,232,0.2);
  color: var(--lavender);
  font-size: 0.65rem;
  letter-spacing: 0.05em;
}

.empty-state {
  text-align: center;
  padding: 3rem 1rem;
  color: var(--muted);
  font-style: italic;
}

.empty-state-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
  opacity: 0.3;
}

/* ── SETTINGS ── */
.settings-section {
  margin-bottom: 2rem;
}

.settings-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 0;
  border-bottom: 1px solid var(--card-border);
}

.settings-label {
  font-size: 0.9rem;
  color: var(--text);
}

.settings-description {
  font-size: 0.75rem;
  color: var(--muted);
  margin-top: 0.25rem;
}

/* ── TOAST ── */
.toast {
  position: fixed;
  bottom: 100px;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(13,17,36,0.95);
  border: 1px solid var(--lavender);
  border-radius: 20px;
  padding: 0.75rem 1.5rem;
  color: var(--lavender);
  font-size: 0.85rem;
  z-index: 1000;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
}

.toast.show {
  opacity: 1;
}

/* ── RESPONSIVE ── */
@media (max-width: 400px) {
  .page-title { font-size: 1.6rem; }
  .breath-orb { width: 160px; height: 160px; }
}
</style>
</head>
<body>
<canvas id="stars-canvas"></canvas>

<div class="shell">
  <!-- MOBILE HEADER -->
  <div class="mobile-header">
    <div class="header-logo">
      <span class="app-name">Swing</span>
    </div>
    <div style="display: flex; gap: 0.5rem; align-items: center;">
      <button class="sound-btn" onclick="toggleSoundMenu()" title="Calm Sounds">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <polygon points="11 5 6 9 2 9 2 15 6 15 11 19 11 5"></polygon>
          <path d="M15.54 8.46a5 5 0 0 1 0 7.07"></path>
          <path d="M19.07 4.93a10 10 0 0 1 0 14.14"></path>
        </svg>
      </button>
      <button class="menu-btn" onclick="toggleNav()">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="3" y1="12" x2="21" y2="12"></line>
          <line x1="3" y1="6" x2="21" y2="6"></line>
          <line x1="3" y1="18" x2="21" y2="18"></line>
        </svg>
      </button>
    </div>
  </div>

  <!-- SOUND MENU POPUP -->
  <div class="sound-menu" id="sound-menu">
    <div class="sound-menu-header">
      <h3>Calm Sounds</h3>
      <button class="sound-close" onclick="toggleSoundMenu()">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="18" y1="6" x2="6" y2="18"></line>
          <line x1="6" y1="6" x2="18" y2="18"></line>
        </svg>
      </button>
    </div>
    <div class="sound-tracks">
      <div class="sound-track" onclick="selectTrackQuick(0, this)">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M3 18v-6a9 9 0 0 1 18 0v6"></path>
          <path d="M21 19a2 2 0 0 1-2 2h-1a2 2 0 0 1-2-2v-3a2 2 0 0 1 2-2h3zM3 19a2 2 0 0 0 2 2h1a2 2 0 0 0 2-2v-3a2 2 0 0 0-2-2H3z"></path>
        </svg>
        <span>Ocean Waves</span>
      </div>
      <div class="sound-track" onclick="selectTrackQuick(1, this)">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="8" y1="19" x2="8" y2="21"></line>
          <line x1="8" y1="13" x2="8" y2="15"></line>
          <line x1="16" y1="19" x2="16" y2="21"></line>
          <line x1="16" y1="13" x2="16" y2="15"></line>
          <line x1="12" y1="21" x2="12" y2="23"></line>
          <line x1="12" y1="15" x2="12" y2="17"></line>
          <path d="M20 16.58A5 5 0 0 0 18 7h-1.26A8 8 0 1 0 4 15.25"></path>
        </svg>
        <span>Gentle Rain</span>
      </div>
      <div class="sound-track" onclick="selectTrackQuick(2, this)">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M12 12c2-2.96 0-7-1-8"></path>
          <path d="M12 12c2 2.96 0 7-1 8"></path>
          <path d="M12 12c-2-2.96 0-7 1-8"></path>
          <path d="M12 12c-2 2.96 0 7 1 8"></path>
        </svg>
        <span>Crackling Fire</span>
      </div>
      <div class="sound-track" onclick="selectTrackQuick(3, this)">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M12 2L2 7l10 5 10-5-10-5z"></path>
          <path d="M2 17l10 5 10-5M2 12l10 5 10-5"></path>
        </svg>
        <span>Forest Ambience</span>
      </div>
      <div class="sound-track" onclick="selectTrackQuick(4, this)">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M18 8h1a4 4 0 0 1 0 8h-1"></path>
          <path d="M2 8h16v9a4 4 0 0 1-4 4H6a4 4 0 0 1-4-4V8z"></path>
          <line x1="6" y1="1" x2="6" y2="4"></line>
          <line x1="10" y1="1" x2="10" y2="4"></line>
          <line x1="14" y1="1" x2="14" y2="4"></line>
        </svg>
        <span>Coffee Shop</span>
      </div>
      <div class="sound-track" onclick="selectTrackQuick(5, this)">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M9.59 4.59A2 2 0 1 1 11 8H2m10.59 11.41A2 2 0 1 0 14 16H2m15.73-8.27A2.5 2.5 0 1 1 19.5 12H2"></path>
        </svg>
        <span>Mountain Wind</span>
      </div>
      <div class="sound-track" onclick="selectTrackQuick(6, this)">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path>
        </svg>
        <span>Night Sounds</span>
      </div>
      <div class="sound-track" onclick="selectTrackQuick(7, this)">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2"></polygon>
        </svg>
        <span>Piano Ambient</span>
      </div>
    </div>
    <div class="sound-controls">
      <button class="sound-play-btn" id="quick-play-btn" onclick="toggleMusicQuick()">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
          <polygon points="5 3 19 12 5 21 5 3"></polygon>
        </svg>
      </button>
      <input type="range" class="sound-volume" id="quick-volume-slider" min="0" max="100" value="50" onchange="updateVolume(this.value)">
    </div>
  </div>

  <!-- NAV OVERLAY -->
  <div class="nav-overlay" onclick="toggleNav()"></div>

  <!-- NAV DRAWER -->
  <div class="nav-drawer">
    <div class="nav-drawer-header">
      <div class="app-name">Swing</div>
      <div class="app-tagline">A Gentle Diary</div>
    </div>

    <div class="nav-section">
      <div class="nav-label">Daily</div>
      <div class="nav-item active" onclick="navigate('home')">
        <span class="nav-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path>
            <polyline points="9 22 9 12 15 12 15 22"></polyline>
          </svg>
        </span> Home
      </div>
      <div class="nav-item" onclick="navigate('win-of-day')">
        <span class="nav-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"></polygon>
          </svg>
        </span> Win of the Day
      </div>
      <div class="nav-item" onclick="navigate('mood-tracker')">
        <span class="nav-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="18" y1="20" x2="18" y2="10"></line>
            <line x1="12" y1="20" x2="12" y2="4"></line>
            <line x1="6" y1="20" x2="6" y2="14"></line>
          </svg>
        </span> Mood Tracker
      </div>
    </div>

    <div class="nav-section">
      <div class="nav-label">Self-Care</div>
      <div class="nav-item" onclick="navigate('compassion')">
        <span class="nav-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"></path>
          </svg>
        </span> Self-Compassion
      </div>
      <div class="nav-item" onclick="navigate('breathing')">
        <span class="nav-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <circle cx="12" cy="12" r="10"></circle>
          </svg>
        </span> Breathing
      </div>
      <div class="nav-item" onclick="navigate('music')">
        <span class="nav-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M9 18V5l12-2v13"></path>
            <circle cx="6" cy="18" r="3"></circle>
            <circle cx="18" cy="16" r="3"></circle>
          </svg>
        </span> Calm Sounds
      </div>
    </div>

    <div class="nav-section">
      <div class="nav-label">CBT Tools</div>
      <div class="nav-item" onclick="navigate('thought-record')">
        <span class="nav-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"></path>
            <path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"></path>
          </svg>
        </span> Thought Record
      </div>
      <div class="nav-item" onclick="navigate('thought-testing')">
        <span class="nav-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <circle cx="11" cy="11" r="8"></circle>
            <path d="m21 21-4.35-4.35"></path>
          </svg>
        </span> Testing Thoughts
      </div>
      <div class="nav-item" onclick="navigate('activation')">
        <span class="nav-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2"></polygon>
          </svg>
        </span> Gentle Action
      </div>
    </div>

    <div class="nav-section">
      <div class="nav-label">More</div>
      <div class="nav-item" onclick="navigate('habits')">
        <span class="nav-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"></path>
            <polyline points="22 4 12 14.01 9 11.01"></polyline>
          </svg>
        </span> Daily Habits
      </div>
      <div class="nav-item" onclick="navigate('entries')">
        <span class="nav-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"></path>
            <path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"></path>
          </svg>
        </span> Past Entries
      </div>
      <div class="nav-item" onclick="navigate('settings')">
        <span class="nav-icon">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <circle cx="12" cy="12" r="3"></circle>
            <path d="M12 1v6m0 6v6m0-18a2 2 0 0 1 2 2v2a2 2 0 0 1-4 0V3a2 2 0 0 1 2-2zm0 12a2 2 0 0 1 2 2v2a2 2 0 0 1-4 0v-2a2 2 0 0 1 2-2z"></path>
            <path d="m4.93 4.93 4.24 4.24m5.66 5.66 4.24 4.24m0-13.14-4.24 4.24m-5.66 5.66-4.24 4.24"></path>
          </svg>
        </span> Settings
      </div>
    </div>
  </div>

  <!-- MAIN CONTENT -->
  <div class="main">
    <!-- ══════════════════════════════════════════════════════════════ -->
    <!-- HOME SCREEN -->
    <!-- ══════════════════════════════════════════════════════════════ -->
    <div id="home" class="screen active">
      <div class="page-header">
        <h1 class="page-title">Welcome back</h1>
        <p class="page-subtitle">How are you feeling today?</p>
      </div>

      <div class="home-grid">
        <div class="home-tile" onclick="navigate('win-of-day')">
          <div class="tile-label">Today's Win</div>
          <div class="tile-content">
            <span class="tile-icon">🌟</span>
            <span id="home-win">Add one</span>
          </div>
        </div>

        <div class="home-tile" onclick="navigate('mood-tracker')">
          <div class="tile-label">Mood Check</div>
          <div class="tile-content">
            <span class="tile-icon">📊</span>
            <span id="home-mood">Track it</span>
          </div>
        </div>

        <div class="home-tile" onclick="navigate('habits')">
          <div class="tile-label">Water</div>
          <div class="tile-content">
            <span class="tile-icon">💧</span>
            <span id="home-water">0 / 8</span>
          </div>
        </div>

        <div class="home-tile" onclick="navigate('habits')">
          <div class="tile-label">Sleep</div>
          <div class="tile-content">
            <span class="tile-icon">🌙</span>
            <span id="home-sleep">—</span>
          </div>
        </div>

        <div class="home-tile" onclick="navigate('habits')">
          <div class="tile-label">Movement</div>
          <div class="tile-content">
            <span class="tile-icon">🏃</span>
            <span id="home-movement">—</span>
          </div>
        </div>

        <div class="home-tile" onclick="navigate('compassion')">
          <div class="tile-label">Self-Compassion</div>
          <div class="tile-content">
            <span class="tile-icon">💝</span>
            <span>Practice</span>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="card-title">✦ Quick Start</div>
        <div style="display: flex; flex-direction: column; gap: 0.5rem;">
          <button class="btn btn-primary" onclick="navigate('thought-record')">Record a Thought</button>
          <button class="btn" onclick="navigate('breathing')">Breathing Exercise</button>
          <button class="btn" onclick="navigate('music')">Play Calm Sounds</button>
        </div>
      </div>
    </div>

    <!-- ══════════════════════════════════════════════════════════════ -->
    <!-- WIN OF THE DAY -->
    <!-- ══════════════════════════════════════════════════════════════ -->
    <div id="win-of-day" class="screen">
      <div class="page-header">
        <h1 class="page-title">Win of the Day</h1>
        <p class="page-subtitle">Every day has at least one win, no matter how small</p>
      </div>

      <div class="card win-input-section">
        <div class="card-title">🌟 Today's Win</div>
        <label>What went well today?</label>
        <textarea id="win-input" placeholder="Maybe you got out of bed, made a meal, talked to a friend, finished a task... all wins count!"></textarea>
        
        <div style="margin-top: 1rem;">
          <button class="btn btn-primary" onclick="saveWin()">Save Win ✦</button>
        </div>
      </div>

      <div class="card">
        <div class="card-title">✨ Past Wins</div>
        <div id="wins-list" class="win-list"></div>
        <div id="no-wins" class="empty-state" style="display: none;">
          <div class="empty-state-icon">🌟</div>
          <div>No wins recorded yet. Add your first one above!</div>
        </div>
      </div>
    </div>

    <!-- ══════════════════════════════════════════════════════════════ -->
    <!-- MOOD TRACKER -->
    <!-- ══════════════════════════════════════════════════════════════ -->
    <div id="mood-tracker" class="screen">
      <div class="page-header">
        <h1 class="page-title">Mood Tracker</h1>
        <p class="page-subtitle">See your mood patterns over time</p>
      </div>

      <div class="card">
        <div class="card-title">📊 This Month</div>
        
        <div class="calendar-header">
          <div>SUN</div>
          <div>MON</div>
          <div>TUE</div>
          <div>WED</div>
          <div>THU</div>
          <div>FRI</div>
          <div>SAT</div>
        </div>
        
        <div id="mood-calendar" class="mood-calendar"></div>

        <div class="mood-legend">
          <div class="legend-item">
            <div class="legend-dot" style="border-color: rgba(106, 212, 148, 0.5); background: rgba(106, 212, 148, 0.15);"></div>
            <span>😊 Great</span>
          </div>
          <div class="legend-item">
            <div class="legend-dot" style="border-color: rgba(201, 184, 232, 0.5); background: rgba(201, 184, 232, 0.15);"></div>
            <span>🙂 Good</span>
          </div>
          <div class="legend-item">
            <div class="legend-dot" style="border-color: rgba(212, 169, 106, 0.5); background: rgba(212, 169, 106, 0.15);"></div>
            <span>😐 Okay</span>
          </div>
          <div class="legend-item">
            <div class="legend-dot" style="border-color: rgba(232, 152, 152, 0.5); background: rgba(232, 152, 152, 0.15);"></div>
            <span>😔 Low</span>
          </div>
          <div class="legend-item">
            <div class="legend-dot" style="border-color: rgba(139, 92, 246, 0.5); background: rgba(139, 92, 246, 0.15);"></div>
            <span>😞 Struggling</span>
          </div>
        </div>
      </div>

      <div class="card">
        <div class="card-title">How are you feeling today?</div>
        <div class="mood-dots">
          <div class="mood-dot" onclick="logMood('great', this)" title="Great">😊</div>
          <div class="mood-dot" onclick="logMood('good', this)" title="Good">🙂</div>
          <div class="mood-dot" onclick="logMood('okay', this)" title="Okay">😐</div>
          <div class="mood-dot" onclick="logMood('low', this)" title="Low">😔</div>
          <div class="mood-dot" onclick="logMood('struggling', this)" title="Struggling">😞</div>
        </div>
      </div>
    </div>

    <!-- ══════════════════════════════════════════════════════════════ -->
    <!-- SELF-COMPASSION EXERCISES -->
    <!-- ══════════════════════════════════════════════════════════════ -->
    <div id="compassion" class="screen">
      <div class="page-header">
        <h1 class="page-title">Self-Compassion</h1>
        <p class="page-subtitle">Practice being kind to yourself</p>
      </div>

      <div class="card">
        <div class="card-title">💝 Guided Prompts</div>
        
        <div class="compassion-prompt">
          <div class="prompt-category">When You're Struggling</div>
          <p>What would you say to a dear friend going through this same situation? Now, can you offer yourself those same words of kindness and understanding?</p>
        </div>

        <div class="compassion-prompt">
          <div class="prompt-category">Acknowledging Your Pain</div>
          <p>Right now, I am experiencing difficulty. This is a moment of suffering. May I be kind to myself in this moment. May I give myself the compassion I need.</p>
        </div>

        <div class="compassion-prompt">
          <div class="prompt-category">Common Humanity</div>
          <p>Everyone struggles sometimes. I am not alone in this. Millions of people feel this way. This is part of being human, and I deserve compassion just like anyone else.</p>
        </div>

        <div class="compassion-prompt">
          <div class="prompt-category">Self-Kindness Practice</div>
          <p>Place your hand over your heart. Feel its warmth. Breathe gently. Say to yourself: "May I be safe. May I be peaceful. May I be kind to myself. May I accept myself as I am."</p>
        </div>

        <div class="compassion-prompt">
          <div class="prompt-category">Reframing Self-Criticism</div>
          <p>Notice the harsh voice in your mind. What is it saying? Now imagine transforming it into the voice of a caring mentor. What would they say instead? How would they encourage you?</p>
        </div>

        <div class="compassion-prompt">
          <div class="prompt-category">Appreciating Yourself</div>
          <p>Name three things you've done well recently, no matter how small. Getting out of bed counts. Making a meal counts. Asking for help counts. You're doing better than you think.</p>
        </div>
      </div>

      <div class="card">
        <div class="card-title">✍️ Your Reflection</div>
        <label>What came up for you during these exercises?</label>
        <textarea id="compassion-reflection" placeholder="Write about your experience..."></textarea>
        
        <div style="margin-top: 1rem;">
          <button class="btn btn-primary" onclick="saveCompassion()">Save Reflection ✦</button>
        </div>
      </div>
    </div>

    <!-- ══════════════════════════════════════════════════════════════ -->
    <!-- MUSIC PLAYER -->
    <!-- ══════════════════════════════════════════════════════════════ -->
    <div id="music" class="screen">
      <div class="page-header">
        <h1 class="page-title">Calm Sounds</h1>
        <p class="page-subtitle">Soothing audio to help you relax</p>
      </div>

      <div class="music-player">
        <div class="player-controls">
          <button class="play-btn" id="music-play-btn" onclick="toggleMusic()">▶</button>
          <div class="track-info">
            <div class="track-title" id="current-track-name">No track playing</div>
            <div class="track-duration" id="current-track-duration">Select a sound below</div>
          </div>
        </div>

        <div class="volume-control">
          <span style="font-size: 0.9rem;">🔉</span>
          <input type="range" class="volume-slider" id="volume-slider" min="0" max="100" value="50" onchange="updateVolume(this.value)">
          <span style="font-size: 0.9rem;">🔊</span>
        </div>
      </div>

      <div class="card">
        <div class="card-title">🎵 Playlist</div>
        <div class="playlist">
          <div class="playlist-item" onclick="selectTrack(0, this)">
            <span class="track-name">🌊 Ocean Waves</span>
            <span style="font-size: 0.75rem; color: var(--muted);">10:00</span>
          </div>
          <div class="playlist-item" onclick="selectTrack(1, this)">
            <span class="track-name">🌧️ Gentle Rain</span>
            <span style="font-size: 0.75rem; color: var(--muted);">10:00</span>
          </div>
          <div class="playlist-item" onclick="selectTrack(2, this)">
            <span class="track-name">🔥 Crackling Fire</span>
            <span style="font-size: 0.75rem; color: var(--muted);">10:00</span>
          </div>
          <div class="playlist-item" onclick="selectTrack(3, this)">
            <span class="track-name">🌲 Forest Ambience</span>
            <span style="font-size: 0.75rem; color: var(--muted);">10:00</span>
          </div>
          <div class="playlist-item" onclick="selectTrack(4, this)">
            <span class="track-name">☕ Coffee Shop</span>
            <span style="font-size: 0.75rem; color: var(--muted);">10:00</span>
          </div>
          <div class="playlist-item" onclick="selectTrack(5, this)">
            <span class="track-name">⛰️ Mountain Wind</span>
            <span style="font-size: 0.75rem; color: var(--muted);">10:00</span>
          </div>
          <div class="playlist-item" onclick="selectTrack(6, this)">
            <span class="track-name">🌌 Night Sounds</span>
            <span style="font-size: 0.75rem; color: var(--muted);">10:00</span>
          </div>
          <div class="playlist-item" onclick="selectTrack(7, this)">
            <span class="track-name">🎹 Piano Ambient</span>
            <span style="font-size: 0.75rem; color: var(--muted);">10:00</span>
          </div>
        </div>
      </div>

      <div class="card" style="background: rgba(201,184,232,0.05); border-color: rgba(201,184,232,0.15);">
        <div style="font-size: 0.85rem; line-height: 1.6; color: var(--muted);">
          <strong style="color: var(--lavender);">💡 Note:</strong> These are placeholder tracks. To add real audio files:
          <ol style="margin: 0.5rem 0 0 1.2rem; line-height: 1.8;">
            <li>Upload .mp3 files to your GitHub repository (e.g., sounds/ocean.mp3)</li>
            <li>Update the playlist array in the JavaScript code</li>
            <li>Add the file paths to each track</li>
          </ol>
        </div>
      </div>
    </div>

    <!-- ══════════════════════════════════════════════════════════════ -->
    <!-- THOUGHT RECORD -->
    <!-- ══════════════════════════════════════════════════════════════ -->
    <div id="thought-record" class="screen">
      <div class="page-header">
        <h1 class="page-title">Thought Record</h1>
        <p class="page-subtitle">Observe your thoughts without judgment</p>
      </div>

      <div class="card">
        <label>What happened?</label>
        <input type="text" id="tr-situation" placeholder="Describe the situation briefly...">

        <label>What emotions did you notice?</label>
        <div id="tr-emotion-tags" class="emotion-tags">
          <span class="emotion-tag" onclick="toggleTag(this)">Anxious</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Sad</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Angry</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Frustrated</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Overwhelmed</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Guilty</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Ashamed</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Scared</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Hopeless</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Lonely</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Worried</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Disappointed</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Embarrassed</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Nervous</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Confused</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Hurt</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Jealous</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Irritated</span>
        </div>

        <label>What thoughts went through your mind?</label>
        <textarea id="tr-thoughts" placeholder="What did you think in that moment?"></textarea>

        <label>How intense was the feeling? (0-10)</label>
        <input type="number" id="tr-intensity" min="0" max="10" placeholder="0 = barely felt it, 10 = overwhelming">

        <label>Alternative perspective (optional)</label>
        <textarea id="tr-alternative" placeholder="Looking back, is there another way to see this?"></textarea>

        <div style="margin-top: 1.5rem;">
          <button class="btn btn-primary" onclick="saveCBTEntry('thought')">Save Record ✦</button>
        </div>
      </div>
    </div>

    <!-- ══════════════════════════════════════════════════════════════ -->
    <!-- THOUGHT TESTING -->
    <!-- ══════════════════════════════════════════════════════════════ -->
    <div id="thought-testing" class="screen">
      <div class="page-header">
        <h1 class="page-title">Testing Thoughts</h1>
        <p class="page-subtitle">Gently examine the evidence</p>
      </div>

      <div class="card">
        <label>What's the thought you want to examine?</label>
        <textarea id="tt-thought" placeholder="Example: 'I'm a failure' or 'Nobody likes me'"></textarea>

        <label>What emotions come with this thought?</label>
        <div id="tt-emotion-tags" class="emotion-tags">
          <span class="emotion-tag" onclick="toggleTag(this)">Anxious</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Sad</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Angry</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Frustrated</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Overwhelmed</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Guilty</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Ashamed</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Scared</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Hopeless</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Lonely</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Worried</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Disappointed</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Embarrassed</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Nervous</span>
          <span class="emotion-tag" onclick="toggleTag(this)">Confused</span>
        </div>

        <label>Evidence FOR the thought</label>
        <textarea id="tt-evidence-for" placeholder="What makes you believe this thought might be true?"></textarea>

        <label>Evidence AGAINST the thought</label>
        <textarea id="tt-evidence-against" placeholder="What suggests this thought might not be completely accurate?"></textarea>

        <label>More balanced or realistic thought</label>
        <textarea id="tt-rational" placeholder="What's a kinder, more balanced way to think about this?"></textarea>

        <div style="margin-top: 1.5rem;">
          <button class="btn btn-primary" onclick="saveCBTEntry('testing')">Save Analysis ✦</button>
        </div>
      </div>
    </div>

    <!-- ══════════════════════════════════════════════════════════════ -->
    <!-- BEHAVIORAL ACTIVATION -->
    <!-- ══════════════════════════════════════════════════════════════ -->
    <div id="activation" class="screen">
      <div class="page-header">
        <h1 class="page-title">Gentle Action</h1>
        <p class="page-subtitle">Small steps toward what matters</p>
      </div>

      <div class="card">
        <label>What do you need or want to do?</label>
        <input type="text" id="ba-task" placeholder="Example: Call a friend, go for a walk, clean one room">

        <label>Why does this matter to you?</label>
        <textarea id="ba-why" placeholder="How might this help you feel better or align with your values?"></textarea>

        <label>Break it into micro-steps</label>
        <div id="ba-steps">
          <div class="action-step-row">
            <div class="step-check" onclick="toggleStep(this)">✓</div>
            <input type="text" placeholder="First tiny step...">
          </div>
          <div class="action-step-row">
            <div class="step-check" onclick="toggleStep(this)">✓</div>
            <input type="text" placeholder="Second tiny step...">
          </div>
        </div>
        <button class="btn" onclick="addStep()" style="margin-top: 0.5rem;">+ Add Step</button>

        <label>When will you start?</label>
        <input type="text" id="ba-when" placeholder="Today at 3pm, tomorrow morning, etc.">

        <label>What might get in the way?</label>
        <textarea id="ba-obstacles" placeholder="Energy, time, motivation, other commitments..."></textarea>

        <label>How can you make it easier?</label>
        <textarea id="ba-micro" placeholder="Set timer for 5 min, ask someone to join, prepare the night before..."></textarea>

        <div style="margin-top: 1.5rem;">
          <button class="btn btn-primary" onclick="saveCBTEntry('activation')">Save Plan ✦</button>
        </div>
      </div>
    </div>

    <!-- ══════════════════════════════════════════════════════════════ -->
    <!-- BREATHING -->
    <!-- ══════════════════════════════════════════════════════════════ -->
    <div id="breathing" class="screen">
      <div class="page-header">
        <h1 class="page-title">Breathing</h1>
        <p class="page-subtitle">Find calm through your breath</p>
      </div>

      <div class="card">
        <div class="card-title">Choose a Pattern</div>
        <div class="pattern-selector">
          <div class="pattern-btn active" onclick="setPattern('box', this)">Box (4-4-4-4)</div>
          <div class="pattern-btn" onclick="setPattern('478', this)">4-7-8</div>
          <div class="pattern-btn" onclick="setPattern('relax', this)">Extended Exhale</div>
        </div>

        <div class="breath-container">
          <div class="breath-instruction" id="breath-instruction">Press start when ready</div>
          
          <div class="breath-orb" id="breath-orb">
            <div class="breath-label" id="breath-label">ready</div>
            <div class="breath-count" id="breath-count"></div>
          </div>

          <div style="display: flex; gap: 1rem;">
            <button class="btn btn-primary" id="breath-start-btn" onclick="startBreathing()">Start</button>
            <button class="btn" id="breath-stop-btn" onclick="stopBreathing()" style="display: none;">Stop</button>
          </div>
        </div>
      </div>
    </div>

    <!-- ══════════════════════════════════════════════════════════════ -->
    <!-- HABITS -->
    <!-- ══════════════════════════════════════════════════════════════ -->
    <div id="habits" class="screen">
      <div class="page-header">
        <h1 class="page-title">Daily Habits</h1>
        <p class="page-subtitle">Track the basics that support you</p>
      </div>

      <div class="card">
        <div class="card-title">💧 Water</div>
        <div id="water-count-label" style="margin-bottom: 0.5rem; font-size: 0.85rem; color: var(--muted);">0 of 8 glasses</div>
        <div id="water-bubbles" class="water-bubbles"></div>
      </div>

      <div class="card">
        <div class="card-title">🌙 Sleep</div>
        <label>Hours slept</label>
        <input type="number" id="h-sleep-hours" min="0" max="24" step="0.5" placeholder="7.5" onchange="updateHomeHabit('sleep', this.value + 'h')">
        
        <label>Quality</label>
        <div class="mood-dots">
          <div class="mood-dot" onclick="selectMood(this, 'sleep')" title="Great">😊</div>
          <div class="mood-dot" onclick="selectMood(this, 'sleep')" title="Good">🙂</div>
          <div class="mood-dot" onclick="selectMood(this, 'sleep')" title="Okay">😐</div>
          <div class="mood-dot" onclick="selectMood(this, 'sleep')" title="Poor">😔</div>
        </div>
      </div>

      <div class="card">
        <div class="card-title">🥗 Nutrition</div>
        <label>How did you eat today?</label>
        <select id="h-nutrition" onchange="updateHomeHabit('nutrition', this.value)">
          <option value="">—</option>
          <option value="nourishing">Nourishing meals</option>
          <option value="okay">Okay</option>
          <option value="struggling">Struggling to eat</option>
          <option value="skipped">Skipped meals</option>
        </select>
      </div>

      <div class="card">
        <div class="card-title">🏃 Movement</div>
        <label>Type</label>
        <input type="text" id="h-movement-type" placeholder="Walking, yoga, stretching, dancing..." onchange="updateHomeHabit('movement', this.value)">
        
        <label>Duration (minutes)</label>
        <input type="number" id="h-movement-mins" min="0" placeholder="20">
      </div>

      <div style="margin-top: 1.5rem;">
        <button class="btn btn-primary" onclick="saveHabits()">Save Today's Habits ✦</button>
      </div>
    </div>

    <!-- ══════════════════════════════════════════════════════════════ -->
    <!-- ENTRIES -->
    <!-- ══════════════════════════════════════════════════════════════ -->
    <div id="entries" class="screen">
      <div class="page-header">
        <h1 class="page-title">Past Entries</h1>
        <p class="page-subtitle">Your journey so far</p>
      </div>

      <div id="entries-list"></div>
      <div id="no-entries" class="empty-state">
        <div class="empty-state-icon">📖</div>
        <div>No entries yet. Start by recording a thought or tracking your mood!</div>
      </div>
    </div>

    <!-- ══════════════════════════════════════════════════════════════ -->
    <!-- SETTINGS -->
    <!-- ══════════════════════════════════════════════════════════════ -->
    <div id="settings" class="screen">
      <div class="page-header">
        <h1 class="page-title">Settings</h1>
        <p class="page-subtitle">Manage your data</p>
      </div>

      <div class="card">
        <div class="card-title">💾 Data Management</div>
        
        <div class="settings-section">
          <button class="btn btn-primary" onclick="exportData()">
            Export All Data
          </button>
          <p style="font-size: 0.75rem; color: var(--muted); margin-top: 0.5rem;">
            Download your entries and habits as a JSON file
          </p>
        </div>

        <div class="settings-section">
          <label for="import-file-input" class="btn" style="cursor: pointer; margin: 0;">
            Import Data
          </label>
          <input type="file" id="import-file-input" accept=".json" onchange="importData(event)" style="display: none;">
          <p style="font-size: 0.75rem; color: var(--muted); margin-top: 0.5rem;">
            Restore from a previous export
          </p>
        </div>
      </div>

      <div class="card">
        <div class="card-title">ℹ️ About</div>
        <p style="line-height: 1.6; color: var(--muted); font-size: 0.85rem;">
          Swing is a gentle space for self-reflection and emotional wellness. 
          All your data is stored locally on your device — nothing is sent to any server.
        </p>
        <p style="line-height: 1.6; color: var(--muted); font-size: 0.85rem; margin-top: 1rem;">
          Version 2.0 · Enhanced with mood tracking, self-compassion exercises, and calm sounds
        </p>
      </div>
    </div>
  </div>
</div>

<!-- TOAST -->
<div id="toast" class="toast"></div>

<script>
// ════════════════════════════════════════════════════════════
// STARFIELD
// ════════════════════════════════════════════════════════════
const canvas = document.getElementById('stars-canvas');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const stars = [];
for (let i = 0; i < 150; i++) {
  stars.push({
    x: Math.random() * canvas.width,
    y: Math.random() * canvas.height,
    r: Math.random() * 1.5,
    opacity: Math.random() * 0.5 + 0.3
  });
}

function drawStars() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  stars.forEach(s => {
    ctx.beginPath();
    ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(232, 224, 240, ${s.opacity})`;
    ctx.fill();
  });
}

setInterval(() => {
  stars.forEach(s => {
    s.opacity = Math.random() * 0.5 + 0.3;
  });
  drawStars();
}, 2000);

drawStars();

window.addEventListener('resize', () => {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  drawStars();
});

// ════════════════════════════════════════════════════════════
// NAVIGATION
// ════════════════════════════════════════════════════════════
function toggleNav() {
  document.querySelector('.nav-drawer').classList.toggle('open');
  document.querySelector('.nav-overlay').classList.toggle('show');
}

function toggleSoundMenu() {
  const menu = document.getElementById('sound-menu');
  menu.classList.toggle('open');
}

// Close sound menu when clicking outside
document.addEventListener('click', (e) => {
  const soundMenu = document.getElementById('sound-menu');
  const soundBtn = document.querySelector('.sound-btn');
  if (soundMenu && soundBtn && !soundMenu.contains(e.target) && !soundBtn.contains(e.target)) {
    soundMenu.classList.remove('open');
  }
});

function navigate(screenId) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById(screenId).classList.add('active');
  
  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  const navItem = Array.from(document.querySelectorAll('.nav-item')).find(n => 
    n.textContent.toLowerCase().includes(screenId.replace('-', ' '))
  );
  if (navItem) navItem.classList.add('active');
  
  toggleNav();
  window.scrollTo(0, 0);
  
  // Initialize screens when navigating to them
  if (screenId === 'mood-tracker') renderMoodCalendar();
  if (screenId === 'win-of-day') renderWins();
  if (screenId === 'entries') renderEntries();
}

// ════════════════════════════════════════════════════════════
// STORAGE
// ════════════════════════════════════════════════════════════
let savedEntries = JSON.parse(localStorage.getItem('swing_entries') || '[]');
let habitData = JSON.parse(localStorage.getItem('swing_habits') || '{}');
let waterCount = 0;
let wins = JSON.parse(localStorage.getItem('swing_wins') || '[]');
let moodData = JSON.parse(localStorage.getItem('swing_moods') || '{}');

// ════════════════════════════════════════════════════════════
// WIN OF THE DAY
// ════════════════════════════════════════════════════════════
function saveWin() {
  const input = document.getElementById('win-input');
  const text = input.value.trim();
  
  if (!text) {
    showToast('Write your win first ✦');
    return;
  }
  
  const win = {
    id: Date.now(),
    date: new Date().toISOString(),
    text: text
  };
  
  wins.unshift(win);
  localStorage.setItem('swing_wins', JSON.stringify(wins));
  input.value = '';
  showToast('Win saved! 🌟');
  renderWins();
  updateHomeWin();
}

function renderWins() {
  const list = document.getElementById('wins-list');
  const empty = document.getElementById('no-wins');
  list.innerHTML = '';
  
  if (wins.length === 0) {
    empty.style.display = 'block';
    return;
  }
  empty.style.display = 'none';
  
  wins.forEach(win => {
    const d = new Date(win.date);
    const day = d.getDate();
    const month = d.toLocaleString('default', { month: 'short' }).toUpperCase();
    
    const el = document.createElement('div');
    el.className = 'win-entry';
    el.innerHTML = `
      <div class="win-date">
        <div class="win-day">${day}</div>
        <div class="win-month">${month}</div>
      </div>
      <div class="win-content">
        <span class="win-icon">✨</span>${win.text}
      </div>
    `;
    list.appendChild(el);
  });
}

function updateHomeWin() {
  const today = new Date().toISOString().slice(0, 10);
  const todayWin = wins.find(w => w.date.startsWith(today));
  document.getElementById('home-win').textContent = todayWin ? '✓ Done' : 'Add one';
}

// ════════════════════════════════════════════════════════════
// MOOD TRACKER
// ════════════════════════════════════════════════════════════
function logMood(mood, el) {
  const today = new Date().toISOString().slice(0, 10);
  moodData[today] = mood;
  localStorage.setItem('swing_moods', JSON.stringify(moodData));
  
  // Update UI
  el.closest('.mood-dots').querySelectorAll('.mood-dot').forEach(d => d.classList.remove('selected'));
  el.classList.add('selected');
  
  showToast('Mood logged ✦');
  renderMoodCalendar();
  updateHomeMood();
}

function renderMoodCalendar() {
  const calendar = document.getElementById('mood-calendar');
  calendar.innerHTML = '';
  
  const today = new Date();
  const year = today.getFullYear();
  const month = today.getMonth();
  
  // Get first day of month and number of days
  const firstDay = new Date(year, month, 1).getDay();
  const daysInMonth = new Date(year, month + 1, 0).getDate();
  
  // Add empty cells for days before month starts
  for (let i = 0; i < firstDay; i++) {
    const emptyDay = document.createElement('div');
    emptyDay.className = 'mood-day';
    calendar.appendChild(emptyDay);
  }
  
  // Add days of month
  for (let day = 1; day <= daysInMonth; day++) {
    const dateStr = `${year}-${String(month + 1).padStart(2, '0')}-${String(day).padStart(2, '0')}`;
    const mood = moodData[dateStr];
    
    const dayEl = document.createElement('div');
    dayEl.className = 'mood-day';
    
    if (mood) {
      dayEl.classList.add('has-mood', `mood-${mood}`);
      const emojis = {
        great: '😊',
        good: '🙂',
        okay: '😐',
        low: '😔',
        struggling: '😞'
      };
      dayEl.innerHTML = `
        <div class="day-number">${day}</div>
        <div class="day-emoji">${emojis[mood]}</div>
      `;
    } else {
      dayEl.innerHTML = `<div class="day-number">${day}</div>`;
    }
    
    calendar.appendChild(dayEl);
  }
}

function updateHomeMood() {
  const today = new Date().toISOString().slice(0, 10);
  const todayMood = moodData[today];
  const emojis = {
    great: '😊',
    good: '🙂',
    okay: '😐',
    low: '😔',
    struggling: '😞'
  };
  document.getElementById('home-mood').textContent = todayMood ? emojis[todayMood] : 'Track it';
}

// ════════════════════════════════════════════════════════════
// SELF-COMPASSION
// ════════════════════════════════════════════════════════════
function saveCompassion() {
  const reflection = document.getElementById('compassion-reflection').value.trim();
  
  if (!reflection) {
    showToast('Write something first ✦');
    return;
  }
  
  const entry = {
    id: Date.now(),
    date: new Date().toISOString(),
    type: 'compassion',
    title: 'Self-Compassion Practice',
    preview: reflection.slice(0, 100),
    tags: ['self-compassion', 'reflection']
  };
  
  savedEntries.unshift(entry);
  localStorage.setItem('swing_entries', JSON.stringify(savedEntries));
  document.getElementById('compassion-reflection').value = '';
  showToast('Reflection saved ✦');
}

// ════════════════════════════════════════════════════════════
// MUSIC PLAYER
// ════════════════════════════════════════════════════════════
const playlist = [
  { name: '🌊 Ocean Waves', file: 'sounds/ocean.mp3', duration: '10:00' },
  { name: '🌧️ Gentle Rain', file: 'sounds/rain.mp3', duration: '10:00' },
  { name: '🔥 Crackling Fire', file: 'sounds/fire.mp3', duration: '10:00' },
  { name: '🌲 Forest Ambience', file: 'sounds/forest.mp3', duration: '10:00' },
  { name: '☕ Coffee Shop', file: 'sounds/coffee.mp3', duration: '10:00' },
  { name: '⛰️ Mountain Wind', file: 'sounds/wind.mp3', duration: '10:00' },
  { name: '🌌 Night Sounds', file: 'sounds/night.mp3', duration: '10:00' },
  { name: '🎹 Piano Ambient', file: 'sounds/piano.mp3', duration: '10:00' }
];

let currentAudio = null;
let currentTrack = -1;
let isPlaying = false;

function selectTrackQuick(index, el) {
  currentTrack = index;
  document.querySelectorAll('.sound-track').forEach(item => item.classList.remove('active'));
  el.classList.add('active');
  
  // Update full music page if exists
  const playlistItems = document.querySelectorAll('.playlist-item');
  if (playlistItems.length > 0) {
    playlistItems.forEach(item => item.classList.remove('active'));
    if (playlistItems[index]) playlistItems[index].classList.add('active');
    document.getElementById('current-track-name').textContent = playlist[index].name;
    document.getElementById('current-track-duration').textContent = playlist[index].duration;
  }
  
  // Stop current audio if playing
  if (currentAudio) {
    currentAudio.pause();
    currentAudio = null;
  }
  
  isPlaying = false;
  updatePlayButtons();
  
  showToast(`Selected: ${playlist[index].name}`);
}

function toggleMusicQuick() {
  if (currentTrack === -1) {
    showToast('Select a track first ✦');
    return;
  }
  
  if (!isPlaying) {
    // Note: Audio files need to be uploaded to work
    showToast('Upload .mp3 files to enable playback ✦');
    isPlaying = true;
    updatePlayButtons();
    document.querySelector('.sound-btn').classList.add('playing');
    
    // Simulated playback (replace with real audio when files are added)
    // currentAudio = new Audio(playlist[currentTrack].file);
    // currentAudio.volume = document.getElementById('quick-volume-slider').value / 100;
    // currentAudio.play();
  } else {
    isPlaying = false;
    updatePlayButtons();
    document.querySelector('.sound-btn').classList.remove('playing');
    // if (currentAudio) currentAudio.pause();
  }
}

function updatePlayButtons() {
  const quickBtn = document.getElementById('quick-play-btn');
  const mainBtn = document.getElementById('music-play-btn');
  
  if (isPlaying) {
    if (quickBtn) quickBtn.innerHTML = '<svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><rect x="6" y="4" width="4" height="16"></rect><rect x="14" y="4" width="4" height="16"></rect></svg>';
    if (mainBtn) mainBtn.textContent = '⏸';
  } else {
    if (quickBtn) quickBtn.innerHTML = '<svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><polygon points="5 3 19 12 5 21 5 3"></polygon></svg>';
    if (mainBtn) mainBtn.textContent = '▶';
  }
}

function selectTrack(index, el) {
  currentTrack = index;
  document.querySelectorAll('.playlist-item').forEach(item => item.classList.remove('active'));
  el.classList.add('active');
  
  // Update quick menu if exists
  const soundTracks = document.querySelectorAll('.sound-track');
  if (soundTracks.length > 0) {
    soundTracks.forEach(item => item.classList.remove('active'));
    if (soundTracks[index]) soundTracks[index].classList.add('active');
  }
  
  document.getElementById('current-track-name').textContent = playlist[index].name;
  document.getElementById('current-track-duration').textContent = playlist[index].duration;
  
  // Stop current audio if playing
  if (currentAudio) {
    currentAudio.pause();
    currentAudio = null;
  }
  
  isPlaying = false;
  updatePlayButtons();
  
  showToast(`Selected: ${playlist[index].name}`);
}

function toggleMusic() {
  if (currentTrack === -1) {
    showToast('Select a track first ✦');
    return;
  }
  
  if (!isPlaying) {
    // Note: Audio files need to be uploaded to work
    showToast('Upload .mp3 files to enable playback ✦');
    isPlaying = true;
    updatePlayButtons();
    document.querySelector('.sound-btn').classList.add('playing');
    
    // Simulated playback (replace with real audio when files are added)
    // currentAudio = new Audio(playlist[currentTrack].file);
    // currentAudio.volume = document.getElementById('volume-slider').value / 100;
    // currentAudio.play();
  } else {
    isPlaying = false;
    updatePlayButtons();
    document.querySelector('.sound-btn').classList.remove('playing');
    // if (currentAudio) currentAudio.pause();
  }
}

function updateVolume(value) {
  if (currentAudio) {
    currentAudio.volume = value / 100;
  }
  // Sync both volume sliders
  const quickSlider = document.getElementById('quick-volume-slider');
  const mainSlider = document.getElementById('volume-slider');
  if (quickSlider) quickSlider.value = value;
  if (mainSlider) mainSlider.value = value;
}

// ════════════════════════════════════════════════════════════
// EMOTION TAGS
// ════════════════════════════════════════════════════════════
function toggleTag(el) { el.classList.toggle('selected'); }

// ════════════════════════════════════════════════════════════
// SAVE CBT ENTRY
// ════════════════════════════════════════════════════════════
function saveCBTEntry(type) {
  let title, preview, tags = [];

  if (type === 'thought') {
    const sit = document.getElementById('tr-situation').value.trim();
    const thoughts = document.getElementById('tr-thoughts').value.trim();
    if (!sit && !thoughts) { showToast('Write something first ✦'); return; }
    title = sit.slice(0, 60) || 'Thought record';
    preview = thoughts.slice(0, 100);
    tags = ['thought record'];
    document.querySelectorAll('#tr-emotion-tags .selected').forEach(t => tags.push(t.textContent));
  } else if (type === 'testing') {
    const thought = document.getElementById('tt-thought').value.trim();
    if (!thought) { showToast('Write the thought first ✦'); return; }
    title = thought.slice(0, 60);
    preview = (document.getElementById('tt-rational').value || '').slice(0, 100);
    tags = ['testing thoughts'];
    document.querySelectorAll('#tt-emotion-tags .selected').forEach(t => tags.push(t.textContent));
  } else if (type === 'activation') {
    const task = document.getElementById('ba-task').value.trim();
    if (!task) { showToast('What do you need to do? ✦'); return; }
    title = task.slice(0, 60);
    preview = document.getElementById('ba-micro').value.slice(0, 100);
    tags = ['gentle action'];
  }

  const entry = {
    id: Date.now(),
    date: new Date().toISOString(),
    type, title, preview, tags
  };

  savedEntries.unshift(entry);
  localStorage.setItem('swing_entries', JSON.stringify(savedEntries));
  showToast('Saved ✦');
}

// ════════════════════════════════════════════════════════════
// ENTRIES
// ════════════════════════════════════════════════════════════
function renderEntries() {
  const list = document.getElementById('entries-list');
  const empty = document.getElementById('no-entries');
  list.innerHTML = '';

  if (savedEntries.length === 0) {
    empty.style.display = 'block';
    return;
  }
  empty.style.display = 'none';

  savedEntries.forEach(entry => {
    const d = new Date(entry.date);
    const day = d.getDate();
    const month = d.toLocaleString('default', { month: 'short' }).toUpperCase();

    const el = document.createElement('div');
    el.className = 'entry-card';
    el.innerHTML = `
      <div class="entry-date-block">
        <div class="entry-day">${day}</div>
        <div class="entry-month">${month}</div>
      </div>
      <div class="entry-body">
        <div class="entry-title">${entry.title}</div>
        ${entry.preview ? `<div class="entry-preview">${entry.preview}</div>` : ''}
        <div class="entry-tags">${entry.tags.map(t => `<span class="entry-tag">${t}</span>`).join('')}</div>
      </div>
    `;
    list.appendChild(el);
  });
}

// ════════════════════════════════════════════════════════════
// HABITS
// ════════════════════════════════════════════════════════════
function initWaterBubbles() {
  const container = document.getElementById('water-bubbles');
  container.innerHTML = '';
  for (let i = 0; i < 8; i++) {
    const b = document.createElement('div');
    b.className = 'bubble' + (i < waterCount ? ' filled' : '');
    b.textContent = '💧';
    b.onclick = () => toggleBubble(b, i);
    container.appendChild(b);
  }
}

function toggleBubble(el, i) {
  el.classList.toggle('filled');
  waterCount = document.querySelectorAll('.bubble.filled').length;
  document.getElementById('water-count-label').textContent = `${waterCount} of 8 glasses`;
  document.getElementById('home-water').textContent = `${waterCount} / 8`;
}

function selectMood(el, group) {
  el.closest('.mood-dots').querySelectorAll('.mood-dot').forEach(d => d.classList.remove('selected'));
  el.classList.add('selected');
}

function updateHomeHabit(key, val) {
  const map = { sleep: 'home-sleep', nutrition: 'home-nutrition', movement: 'home-movement' };
  if (map[key]) document.getElementById(map[key]).textContent = val || '—';
}

function saveHabits() {
  const today = new Date().toISOString().slice(0, 10);
  habitData[today] = {
    sleep: document.getElementById('h-sleep-hours').value,
    water: waterCount,
    nutrition: document.getElementById('h-nutrition').value,
    movement: document.getElementById('h-movement-type').value,
    movementMins: document.getElementById('h-movement-mins').value
  };
  localStorage.setItem('swing_habits', JSON.stringify(habitData));
  showToast('Habits saved ✦');

  // Update home tiles
  if (habitData[today].sleep) document.getElementById('home-sleep').textContent = habitData[today].sleep + 'h';
  if (habitData[today].movement) document.getElementById('home-movement').textContent = habitData[today].movement;
}

initWaterBubbles();

// ════════════════════════════════════════════════════════════
// BREATHING
// ════════════════════════════════════════════════════════════
const patterns = {
  box:    { inhale: 4, hold1: 4, exhale: 4, hold2: 4, name: 'Box Breathing' },
  '478':  { inhale: 4, hold1: 7, exhale: 8, hold2: 0, name: '4-7-8' },
  relax:  { inhale: 4, hold1: 0, exhale: 8, hold2: 0, name: 'Extended Exhale' }
};

let currentPattern = patterns.box;
let breathTimer = null;
let breathRunning = false;

function setPattern(key, el) {
  currentPattern = patterns[key];
  document.querySelectorAll('.pattern-btn').forEach(b => b.classList.remove('active'));
  el.classList.add('active');
  if (breathRunning) { stopBreathing(); }
}

function startBreathing() {
  if (breathRunning) return;
  breathRunning = true;
  document.getElementById('breath-start-btn').style.display = 'none';
  document.getElementById('breath-stop-btn').style.display = 'inline-flex';
  runBreathCycle();
}

function stopBreathing() {
  breathRunning = false;
  clearTimeout(breathTimer);
  document.getElementById('breath-start-btn').style.display = 'inline-flex';
  document.getElementById('breath-stop-btn').style.display = 'none';
  document.getElementById('breath-instruction').textContent = 'Press start when ready';
  document.getElementById('breath-count').textContent = '';
  document.getElementById('breath-label').textContent = 'ready';
  const orb = document.getElementById('breath-orb');
  orb.className = 'breath-orb';
}

function runBreathCycle() {
  if (!breathRunning) return;
  const p = currentPattern;
  const phases = [
    { label: 'Inhale', orbLabel: '↑', time: p.inhale, class: 'inhale' },
    ...(p.hold1 > 0 ? [{ label: 'Hold', orbLabel: '—', time: p.hold1, class: 'hold' }] : []),
    { label: 'Exhale', orbLabel: '↓', time: p.exhale, class: 'exhale' },
    ...(p.hold2 > 0 ? [{ label: 'Hold', orbLabel: '—', time: p.hold2, class: 'hold' }] : [])
  ];

  let phaseIdx = 0;

  function runPhase() {
    if (!breathRunning) return;
    if (phaseIdx >= phases.length) { phaseIdx = 0; }
    const phase = phases[phaseIdx];
    document.getElementById('breath-instruction').textContent = phase.label;
    document.getElementById('breath-label').textContent = phase.orbLabel;
    const orb = document.getElementById('breath-orb');
    orb.className = 'breath-orb ' + phase.class;

    let secs = phase.time;
    document.getElementById('breath-count').textContent = secs;

    const tick = () => {
      if (!breathRunning) return;
      secs--;
      document.getElementById('breath-count').textContent = secs > 0 ? secs : '';
      if (secs <= 0) {
        phaseIdx++;
        breathTimer = setTimeout(runPhase, 200);
      } else {
        breathTimer = setTimeout(tick, 1000);
      }
    };
    breathTimer = setTimeout(tick, 1000);
  }
  runPhase();
}

// ════════════════════════════════════════════════════════════
// BEHAVIORAL ACTIVATION STEPS
// ════════════════════════════════════════════════════════════
function addStep() {
  const container = document.getElementById('ba-steps');
  const row = document.createElement('div');
  row.className = 'action-step-row';
  row.innerHTML = `
    <div class="step-check" onclick="toggleStep(this)">✓</div>
    <input type="text" placeholder="Another step...">
  `;
  container.appendChild(row);
}

function toggleStep(el) { el.classList.toggle('done'); }

// ════════════════════════════════════════════════════════════
// EXPORT / IMPORT DATA
// ════════════════════════════════════════════════════════════
function exportData() {
  const data = {
    entries: savedEntries,
    habits: habitData,
    wins: wins,
    moods: moodData,
    exportDate: new Date().toISOString(),
    version: '2.0'
  };
  
  const jsonStr = JSON.stringify(data, null, 2);
  const blob = new Blob([jsonStr], { type: 'application/json' });
  const url = URL.createObjectURL(blob);
  
  const a = document.createElement('a');
  a.href = url;
  a.download = `swing-diary-${new Date().toISOString().slice(0, 10)}.json`;
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);
  
  showToast('Data exported ✦');
}

function importData(event) {
  const file = event.target.files[0];
  if (!file) return;
  
  const reader = new FileReader();
  reader.onload = (e) => {
    try {
      const data = JSON.parse(e.target.result);
      
      if (data.entries) {
        savedEntries = data.entries;
        localStorage.setItem('swing_entries', JSON.stringify(savedEntries));
      }
      
      if (data.habits) {
        habitData = data.habits;
        localStorage.setItem('swing_habits', JSON.stringify(habitData));
      }

      if (data.wins) {
        wins = data.wins;
        localStorage.setItem('swing_wins', JSON.stringify(wins));
      }

      if (data.moods) {
        moodData = data.moods;
        localStorage.setItem('swing_moods', JSON.stringify(moodData));
      }
      
      showToast('Data imported successfully ✦');
      renderEntries();
      renderWins();
      renderMoodCalendar();
      
    } catch (err) {
      showToast('Error importing data ✦');
      console.error('Import error:', err);
    }
  };
  
  reader.readAsText(file);
  event.target.value = '';
}

// ════════════════════════════════════════════════════════════
// TOAST
// ════════════════════════════════════════════════════════════
let toastTimeout;
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  clearTimeout(toastTimeout);
  toastTimeout = setTimeout(() => t.classList.remove('show'), 2500);
}

// ════════════════════════════════════════════════════════════
// INITIALIZE
// ════════════════════════════════════════════════════════════
updateHomeWin();
updateHomeMood();
</script>
</body>
</html>
