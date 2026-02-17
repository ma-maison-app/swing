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

<script>
// ══════════════════════════════════════════════════════════════════════════════
// ██████╗ FIREBASE REST API — No SDK needed
// ══════════════════════════════════════════════════════════════════════════════
const FirebaseREST = {
  config: null,
  currentUser: null,

  init: async function(config) {
    this.config = config;
    this.currentUser = await this.getStoredUser();
    return this;
  },

  signUp: async function(email, password) {
    const url = `https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=${this.config.apiKey}`;
    const response = await fetch(url, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ email, password, returnSecureToken: true })
    });
    const data = await response.json();
    if (data.error) throw new Error(data.error.message);
    this.currentUser = { uid: data.localId, email: data.email, token: data.idToken, refreshToken: data.refreshToken };
    await this.storeUser(this.currentUser);
    if (window._authCallback) window._authCallback(this.currentUser);
    return this.currentUser;
  },

  signIn: async function(email, password) {
    const url = `https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=${this.config.apiKey}`;
    const response = await fetch(url, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ email, password, returnSecureToken: true })
    });
    const data = await response.json();
    if (data.error) throw new Error(data.error.message);
    this.currentUser = { uid: data.localId, email: data.email, token: data.idToken, refreshToken: data.refreshToken };
    await this.storeUser(this.currentUser);
    if (window._authCallback) window._authCallback(this.currentUser);
    return this.currentUser;
  },

  signOut: async function() {
    this.currentUser = null;
    this._memoryStore = {};
    try { const db = await this._getDB(); const t = db.transaction([this._storeName], 'readwrite'); t.objectStore(this._storeName).delete('firebase_user'); } catch(e) {}
    try { sessionStorage.removeItem('firebase_user'); } catch(e) {}
    if (window._authCallback) window._authCallback(null);
  },

  setDocument: async function(collection, docId, data) {
    if (!this.currentUser) throw new Error('Not authenticated');
    await this.refreshTokenIfNeeded();
    const url = `https://firestore.googleapis.com/v1/projects/${this.config.projectId}/databases/(default)/documents/${collection}/${docId}`;
    const response = await fetch(url, {
      method: 'PATCH',
      headers: { 'Content-Type': 'application/json', 'Authorization': `Bearer ${this.currentUser.token}` },
      body: JSON.stringify({ fields: this.toFirestoreFormat(data) })
    });
    const result = await response.json();
    if (result.error) throw new Error(result.error.message || JSON.stringify(result.error));
    return result;
  },

  getDocument: async function(collection, docId) {
    if (!this.currentUser) throw new Error('Not authenticated');
    await this.refreshTokenIfNeeded();
    const url = `https://firestore.googleapis.com/v1/projects/${this.config.projectId}/databases/(default)/documents/${collection}/${docId}`;
    const response = await fetch(url, { headers: { 'Authorization': `Bearer ${this.currentUser.token}` } });
    const result = await response.json();
    if (result.error) { if (result.error.code === 404) return null; throw new Error(result.error.message); }
    return this.fromFirestoreFormat(result.fields);
  },

  toFirestoreFormat: function(obj) {
    const result = {};
    for (const [key, value] of Object.entries(obj)) {
      if (value === null) result[key] = { nullValue: null };
      else if (typeof value === 'string') result[key] = { stringValue: value };
      else if (typeof value === 'number') result[key] = { doubleValue: value };
      else if (typeof value === 'boolean') result[key] = { booleanValue: value };
      else if (Array.isArray(value)) {
        result[key] = { arrayValue: { values: value.map(item => {
          if (typeof item === 'object' && item !== null) return { mapValue: { fields: this.toFirestoreFormat(item) } };
          if (typeof item === 'string') return { stringValue: item };
          if (typeof item === 'number') return { doubleValue: item };
          if (typeof item === 'boolean') return { booleanValue: item };
          return { stringValue: String(item) };
        })}};
      } else if (typeof value === 'object') result[key] = { mapValue: { fields: this.toFirestoreFormat(value) } };
      else result[key] = { stringValue: String(value) };
    }
    return result;
  },

  fromFirestoreFormat: function(fields) {
    if (!fields) return null;
    const result = {};
    for (const [key, value] of Object.entries(fields)) {
      if (value.stringValue !== undefined) result[key] = value.stringValue;
      else if (value.doubleValue !== undefined) result[key] = value.doubleValue;
      else if (value.integerValue !== undefined) result[key] = parseInt(value.integerValue);
      else if (value.booleanValue !== undefined) result[key] = value.booleanValue;
      else if (value.nullValue !== undefined) result[key] = null;
      else if (value.arrayValue) {
        result[key] = value.arrayValue.values ? value.arrayValue.values.map(item => {
          if (item.mapValue) return this.fromFirestoreFormat(item.mapValue.fields);
          if (item.stringValue !== undefined) return item.stringValue;
          if (item.doubleValue !== undefined) return item.doubleValue;
          if (item.booleanValue !== undefined) return item.booleanValue;
          return item;
        }) : [];
      } else if (value.mapValue) result[key] = this.fromFirestoreFormat(value.mapValue.fields);
    }
    return result;
  },

  _memoryStore: {},
  _dbName: 'ThoughtRecordDB',
  _storeName: 'auth',

  _getDB: async function() {
    return new Promise((resolve, reject) => {
      const request = indexedDB.open(this._dbName, 1);
      request.onerror = () => reject(request.error);
      request.onsuccess = () => resolve(request.result);
      request.onupgradeneeded = (e) => {
        const db = e.target.result;
        if (!db.objectStoreNames.contains(this._storeName)) db.createObjectStore(this._storeName);
      };
    });
  },

  storeUser: async function(user) {
    const userData = { ...user, timestamp: Date.now() };
    this._memoryStore.firebase_user = userData;
    try {
      const db = await this._getDB();
      const t = db.transaction([this._storeName], 'readwrite');
      t.objectStore(this._storeName).put(userData, 'firebase_user');
    } catch(e) {
      try { sessionStorage.setItem('firebase_user', JSON.stringify(userData)); } catch(e2) {}
    }
  },

  getStoredUser: async function() {
    if (this._memoryStore.firebase_user) {
      const u = this._memoryStore.firebase_user;
      if (Date.now() - u.timestamp < 60 * 60 * 1000) return u;
    }
    try {
      const db = await this._getDB();
      const t = db.transaction([this._storeName], 'readonly');
      const request = t.objectStore(this._storeName).get('firebase_user');
      const user = await new Promise((res, rej) => { request.onsuccess = () => res(request.result); request.onerror = () => rej(request.error); });
      if (user && Date.now() - user.timestamp < 60 * 60 * 1000) { this._memoryStore.firebase_user = user; return user; }
    } catch(e) {}
    try {
      const stored = sessionStorage.getItem('firebase_user');
      if (stored) { const user = JSON.parse(stored); if (Date.now() - user.timestamp < 60 * 60 * 1000) { this._memoryStore.firebase_user = user; return user; } }
    } catch(e) {}
    return null;
  },

  refreshTokenIfNeeded: async function() {
    if (!this.currentUser) return;
    const stored = this._memoryStore.firebase_user;
    if (!stored || Date.now() - stored.timestamp < 50 * 60 * 1000) return;
    const url = `https://securetoken.googleapis.com/v1/token?key=${this.config.apiKey}`;
    const response = await fetch(url, { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify({ grant_type: 'refresh_token', refresh_token: this.currentUser.refreshToken }) });
    const data = await response.json();
    if (data.error) { await this.signOut(); throw new Error('Session expired'); }
    this.currentUser.token = data.id_token;
    this.currentUser.refreshToken = data.refresh_token;
    await this.storeUser(this.currentUser);
  }
};

// ══════════════════════════════════════════════════════════════════════════════
// 🔧 YOUR FIREBASE CONFIG — paste from Firebase console
// ══════════════════════════════════════════════════════════════════════════════
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  projectId: "YOUR_PROJECT_ID",
};

(async () => {
  await FirebaseREST.init(firebaseConfig);
  window._authCallback = async (user) => {
    if (user) {
      document.getElementById('auth-overlay').style.display = 'none';
      document.getElementById('app').style.display = 'block';
      document.getElementById('user-email').textContent = user.email;
      await loadRecordsFromCloud();
    } else {
      document.getElementById('auth-overlay').style.display = 'flex';
      document.getElementById('app').style.display = 'none';
    }
  };
  // Check stored session
  const storedUser = await FirebaseREST.getStoredUser();
  if (storedUser) {
    FirebaseREST.currentUser = storedUser;
    window._authCallback(storedUser);
  } else {
    window._authCallback(null);
  }
})();
</script>

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
body { font-family: 'DM Sans', sans-serif; background: var(--night); color: var(--text); min-height: 100vh; overflow-x: hidden; padding: 2rem 1rem; }
#stars-canvas { position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 0; }

/* ── AUTH OVERLAY ── */
#auth-overlay {
  position: fixed; top: 0; left: 0; width: 100%; height: 100%;
  background: rgba(13,17,36,0.97);
  display: flex; align-items: center; justify-content: center;
  z-index: 100; backdrop-filter: blur(20px);
}
.auth-box {
  background: rgba(255,255,255,0.05);
  border: 1px solid var(--card-border);
  border-radius: var(--radius);
  padding: 2.5rem;
  width: 100%; max-width: 400px;
  backdrop-filter: blur(20px);
}
.auth-title {
  font-family: 'Allura', cursive;
  font-size: 2.5rem;
  color: var(--moon);
  text-align: center;
  margin-bottom: 0.5rem;
}
.auth-subtitle {
  text-align: center;
  color: var(--muted);
  font-size: 0.9rem;
  margin-bottom: 2rem;
}
.auth-tabs {
  display: flex;
  border-bottom: 1px solid var(--card-border);
  margin-bottom: 1.5rem;
}
.auth-tab {
  flex: 1; background: none; border: none;
  color: var(--muted); padding: 0.75rem;
  font-family: 'DM Sans', sans-serif; font-size: 0.95rem; font-weight: 500;
  cursor: pointer; border-bottom: 2px solid transparent;
  transition: all 0.2s;
}
.auth-tab.active { color: var(--lavender); border-bottom-color: var(--lavender); }
.auth-input {
  width: 100%;
  background: rgba(255,255,255,0.04);
  border: 1px solid var(--card-border);
  border-radius: 10px;
  padding: 0.85rem 1rem;
  color: var(--text);
  font-family: 'DM Sans', sans-serif;
  font-size: 1rem;
  margin-bottom: 0.75rem;
  transition: border-color 0.2s;
}
.auth-input:focus { outline: none; border-color: var(--lavender); }
.auth-input::placeholder { color: var(--muted); }
.auth-btn {
  width: 100%;
  background: linear-gradient(135deg, var(--lavender), var(--blush));
  color: var(--night);
  border: none; border-radius: 10px;
  padding: 0.9rem; font-family: 'DM Sans', sans-serif;
  font-size: 1rem; font-weight: 600;
  cursor: pointer; margin-top: 0.5rem;
  transition: all 0.2s;
}
.auth-btn:hover { transform: translateY(-1px); box-shadow: 0 6px 20px rgba(201,184,232,0.3); }
.auth-btn:disabled { opacity: 0.6; cursor: not-allowed; transform: none; }
.auth-error {
  color: #ff9bb3;
  font-size: 0.875rem;
  text-align: center;
  margin-top: 0.75rem;
  min-height: 1.2em;
}

/* ── APP ── */
#app { display: none; }
.container { max-width: 700px; margin: 0 auto; position: relative; z-index: 1; }

/* ── HEADER ── */
.header { text-align: center; margin-bottom: 3rem; position: relative; }
.title { font-family: 'Allura', cursive; font-size: 3rem; color: var(--moon); margin-bottom: 0.5rem; }
.user-bar {
  display: flex; align-items: center; justify-content: center; gap: 0.75rem;
  font-size: 0.85rem; color: var(--muted);
}
.sync-indicator {
  display: inline-flex; align-items: center; gap: 0.3rem;
  font-size: 0.8rem; color: var(--muted);
}
.sync-dot {
  width: 7px; height: 7px; border-radius: 50%;
  background: #6ee7b7; box-shadow: 0 0 6px #6ee7b7;
  animation: pulse 2s infinite;
}
.sync-dot.syncing { background: var(--gold); box-shadow: 0 0 6px var(--gold); }
.sync-dot.error { background: #ff9bb3; box-shadow: 0 0 6px #ff9bb3; animation: none; }
@keyframes pulse { 0%,100% { opacity:1; } 50% { opacity:0.4; } }

.signout-btn {
  background: none; border: 1px solid var(--card-border);
  color: var(--muted); padding: 0.3rem 0.8rem;
  border-radius: 20px; font-size: 0.8rem; cursor: pointer;
  font-family: 'DM Sans', sans-serif;
  transition: all 0.2s;
}
.signout-btn:hover { border-color: var(--blush); color: var(--blush); }

/* ── NAVIGATION TABS ── */
.nav-tabs { display: flex; gap: 0.5rem; margin-bottom: 2rem; border-bottom: 1px solid var(--card-border); flex-wrap: wrap; }
.nav-tab { background: none; border: none; color: var(--muted); font-family: 'DM Sans', sans-serif; font-size: 0.95rem; font-weight: 500; padding: 0.75rem 1.25rem; cursor: pointer; border-bottom: 2px solid transparent; transition: all 0.3s ease; display: flex; align-items: center; gap: 0.5rem; }
.nav-tab:hover { color: var(--lavender); }
.nav-tab.active { color: var(--lavender); border-bottom-color: var(--lavender); }
.nav-tab svg { width: 18px; height: 18px; }

/* ── TAB CONTENT ── */
.tab-content { display: none; }
.tab-content.active { display: block; }

/* ── CARD ── */
.card { background: var(--card); border: 1px solid var(--card-border); border-radius: var(--radius); padding: 2rem; backdrop-filter: blur(20px); margin-bottom: 1.5rem; }

/* ── FORM SECTIONS ── */
.section { margin-bottom: 2rem; }
.section:last-child { margin-bottom: 0; }
.section-label { font-family: 'Playfair Display', serif; font-size: 1.4rem; font-weight: 700; color: var(--lavender); margin-bottom: 0.75rem; display: block; letter-spacing: 0.3px; }
.helper-text { font-size: 0.875rem; color: var(--muted); margin-bottom: 0.5rem; font-style: italic; }

/* ── INPUTS ── */
textarea, input[type="text"] { width: 100%; background: rgba(255,255,255,0.02); border: 1px solid var(--card-border); border-radius: 12px; padding: 1rem; color: var(--text); font-family: 'DM Sans', sans-serif; font-size: 1rem; line-height: 1.6; resize: vertical; transition: border-color 0.3s ease; }
textarea { min-height: 100px; }
textarea:focus, input:focus { outline: none; border-color: var(--lavender); }
textarea::placeholder, input::placeholder { color: var(--muted); }

/* ── EMOTION INTENSITY ── */
.emotion-row { display: flex; gap: 1rem; align-items: flex-start; }
.emotion-row > div:first-child { flex: 2; }
.emotion-row > div:last-child { flex: 1; }
.intensity-label { font-size: 0.875rem; color: var(--muted); margin-bottom: 0.5rem; display: block; }
input[type="range"] { width: 100%; height: 6px; background: rgba(255,255,255,0.1); border-radius: 3px; outline: none; -webkit-appearance: none; margin: 0.5rem 0; }
input[type="range"]::-webkit-slider-thumb { -webkit-appearance: none; appearance: none; width: 20px; height: 20px; background: var(--lavender); border-radius: 50%; cursor: pointer; }
input[type="range"]::-moz-range-thumb { width: 20px; height: 20px; background: var(--lavender); border-radius: 50%; cursor: pointer; border: none; }
.intensity-value { text-align: center; color: var(--lavender); font-size: 1.5rem; font-weight: 500; margin-top: 0.5rem; }

/* ── EVIDENCE GRID ── */
.evidence-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; margin-bottom: 2rem; }
@media (max-width: 600px) { .evidence-grid { grid-template-columns: 1fr; } }
.evidence-box { background: rgba(255,255,255,0.02); border: 1px solid var(--card-border); border-radius: 12px; padding: 1.5rem; }
.evidence-title { font-family: 'Playfair Display', serif; font-size: 1.2rem; font-weight: 600; color: var(--blush); margin-bottom: 0.75rem; }
.evidence-box.against .evidence-title { color: var(--gold); }

/* ── DISTORTIONS ── */
.distortion-tags { display: flex; flex-wrap: wrap; gap: 0.5rem; margin-top: 0.5rem; }
.distortion-tag { background: rgba(201,184,232,0.1); border: 1px solid rgba(201,184,232,0.2); color: var(--lavender); padding: 0.5rem 1rem; border-radius: 20px; font-size: 0.875rem; cursor: pointer; transition: all 0.3s ease; }
.distortion-tag:hover { background: rgba(201,184,232,0.2); border-color: var(--lavender); }
.distortion-tag.selected { background: var(--lavender); color: var(--night); border-color: var(--lavender); }

/* ── EXPANDABLE DISTORTION INFO ── */
.distortion-info-trigger { display: inline-flex; align-items: center; gap: 0.5rem; color: var(--muted); font-size: 0.875rem; cursor: pointer; margin-top: 0.75rem; padding: 0.5rem 0.75rem; border-radius: 8px; transition: all 0.2s ease; }
.distortion-info-trigger:hover { color: var(--lavender); background: rgba(201,184,232,0.05); }
.distortion-info-trigger svg { width: 16px; height: 16px; transition: transform 0.3s ease; }
.distortion-info-trigger.expanded svg:last-child { transform: rotate(180deg); }
.distortion-details { max-height: 0; overflow: hidden; transition: max-height 0.4s ease; margin-top: 0.5rem; }
.distortion-details.expanded { max-height: 2000px; }
.distortion-item { background: rgba(255,255,255,0.02); border: 1px solid var(--card-border); border-radius: 10px; padding: 1rem; margin-bottom: 0.75rem; }
.distortion-item:last-child { margin-bottom: 0; }
.distortion-name { font-family: 'Playfair Display', serif; font-weight: 600; color: var(--lavender); font-size: 1rem; margin-bottom: 0.5rem; }
.distortion-description { font-size: 0.875rem; color: var(--text); line-height: 1.6; margin-bottom: 0.75rem; }
.distortion-example { font-size: 0.85rem; color: var(--muted); font-style: italic; line-height: 1.5; padding-left: 1rem; border-left: 2px solid var(--card-border); }

/* ── CONCLUSION HIGHLIGHT ── */
.conclusion-box { background: linear-gradient(135deg, rgba(201,184,232,0.1) 0%, rgba(232,200,212,0.1) 100%); border: 2px solid var(--lavender); border-radius: 12px; padding: 1.5rem; }

/* ── ACTION BUTTONS ── */
.actions { display: flex; gap: 1rem; margin-top: 2rem; justify-content: center; flex-wrap: wrap; }
.btn { padding: 1rem 2rem; border-radius: 12px; border: none; font-family: 'DM Sans', sans-serif; font-size: 1rem; font-weight: 500; cursor: pointer; transition: all 0.3s ease; display: inline-flex; align-items: center; gap: 0.5rem; }
.btn-primary { background: linear-gradient(135deg, var(--lavender) 0%, var(--blush) 100%); color: var(--night); }
.btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 20px rgba(201,184,232,0.3); }
.btn-secondary { background: rgba(255,255,255,0.05); color: var(--text); border: 1px solid var(--card-border); }
.btn-secondary:hover { background: rgba(255,255,255,0.08); border-color: var(--lavender); }

/* ── SVG ICON BUTTONS ── */
.icon-btn { background: rgba(255,255,255,0.05); border: 1px solid var(--card-border); border-radius: 8px; padding: 0.5rem 0.75rem; cursor: pointer; transition: all 0.2s ease; display: inline-flex; align-items: center; gap: 0.4rem; font-size: 0.875rem; color: var(--text); }
.icon-btn:hover { background: rgba(255,255,255,0.1); border-color: var(--lavender); color: var(--lavender); }
.icon-btn svg { width: 16px; height: 16px; stroke: currentColor; fill: none; stroke-width: 2; stroke-linecap: round; stroke-linejoin: round; }
.icon-btn-delete:hover { border-color: var(--blush); color: var(--blush); }

/* ── SAVED MESSAGE ── */
.saved-msg { position: fixed; top: 2rem; right: 2rem; background: var(--lavender); color: var(--night); padding: 1rem 1.5rem; border-radius: 12px; font-weight: 500; opacity: 0; transform: translateY(-20px); transition: all 0.3s ease; z-index: 1000; box-shadow: 0 8px 20px rgba(0,0,0,0.3); }
.saved-msg.show { opacity: 1; transform: translateY(0); }
.saved-msg.error { background: #ff9bb3; }

/* ── HISTORY SECTION ── */
.no-records { text-align: center; color: var(--muted); padding: 2rem; font-style: italic; }
.record-card { background: var(--card); border: 1px solid var(--card-border); border-radius: var(--radius); padding: 1.5rem; margin-bottom: 1rem; backdrop-filter: blur(20px); }
.record-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 1rem; padding-bottom: 1rem; border-bottom: 1px solid var(--card-border); }
.record-date { font-family: 'Cormorant Garamond', serif; color: var(--muted); font-size: 0.95rem; }
.record-actions { display: flex; gap: 0.5rem; }
.record-content { display: grid; gap: 1rem; }
.record-field { display: grid; gap: 0.4rem; }
.record-field-label { font-family: 'Playfair Display', serif; font-weight: 600; color: var(--lavender); font-size: 0.95rem; }
.record-field-value { color: var(--text); line-height: 1.6; font-size: 0.95rem; }
.record-distortions { display: flex; flex-wrap: wrap; gap: 0.4rem; }
.record-distortion-tag { background: rgba(201,184,232,0.15); border: 1px solid rgba(201,184,232,0.25); color: var(--lavender); padding: 0.35rem 0.75rem; border-radius: 16px; font-size: 0.8rem; }

/* ── EDIT MODE ── */
.edit-mode { background: rgba(201,184,232,0.05); border-color: var(--lavender); }
.edit-form { display: none; margin-top: 1rem; padding-top: 1rem; border-top: 1px solid var(--card-border); }
.edit-form.active { display: block; }
.edit-form textarea { margin-bottom: 0.75rem; }
.edit-actions { display: flex; gap: 0.5rem; margin-top: 1rem; }

/* ── INSIGHTS & STATS ── */
.stats-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 1rem; margin-bottom: 2rem; }
.stat-card { background: rgba(255,255,255,0.02); border: 1px solid var(--card-border); border-radius: 12px; padding: 1.5rem; text-align: center; }
.stat-value { font-family: 'Playfair Display', serif; font-size: 2rem; font-weight: 700; color: var(--lavender); margin-bottom: 0.5rem; }
.stat-label { font-size: 0.875rem; color: var(--muted); }
.chart-container { background: rgba(255,255,255,0.02); border: 1px solid var(--card-border); border-radius: 12px; padding: 1.5rem; margin-bottom: 1.5rem; position: relative; height: 300px; }
.pattern-list { display: grid; gap: 0.75rem; }
.pattern-item { display: flex; justify-content: space-between; align-items: center; background: rgba(255,255,255,0.02); border: 1px solid var(--card-border); border-radius: 10px; padding: 1rem; }
.pattern-name { font-weight: 500; color: var(--text); }
.pattern-count { background: var(--lavender); color: var(--night); padding: 0.25rem 0.75rem; border-radius: 12px; font-size: 0.875rem; font-weight: 600; }

/* ── QUICK EXAMPLES ── */
.example-card { background: rgba(201,184,232,0.05); border: 1px solid rgba(201,184,232,0.2); border-radius: 12px; padding: 1.25rem; margin-bottom: 1rem; cursor: pointer; transition: all 0.3s ease; }
.example-card:hover { background: rgba(201,184,232,0.1); border-color: var(--lavender); transform: translateY(-2px); }
.example-thought { font-family: 'Cormorant Garamond', serif; font-size: 1.1rem; color: var(--text); margin-bottom: 0.75rem; font-style: italic; }
.example-response { font-size: 0.9rem; color: var(--muted); line-height: 1.6; }
.example-tag { display: inline-block; background: rgba(201,184,232,0.2); color: var(--lavender); padding: 0.25rem 0.75rem; border-radius: 12px; font-size: 0.75rem; margin-top: 0.75rem; margin-right: 0.4rem; }

/* ── TOOLKIT ── */
.toolkit-grid { display: grid; gap: 1rem; }
.toolkit-item { background: rgba(255,255,255,0.02); border: 1px solid var(--card-border); border-radius: 12px; padding: 1.5rem; transition: all 0.3s ease; }
.toolkit-item:hover { border-color: var(--lavender); background: rgba(201,184,232,0.05); }
.toolkit-title { font-family: 'Playfair Display', serif; font-weight: 600; color: var(--lavender); font-size: 1.1rem; margin-bottom: 0.75rem; }
.toolkit-content { color: var(--text); line-height: 1.6; font-size: 0.95rem; }
.toolkit-steps { list-style: none; padding-left: 0; margin-top: 0.5rem; }
.toolkit-steps li { padding: 0.5rem 0; padding-left: 1.5rem; position: relative; }
.toolkit-steps li:before { content: "•"; position: absolute; left: 0; color: var(--lavender); font-weight: bold; }

/* ── RESPONSIVE ── */
@media (max-width: 600px) {
  .title { font-size: 2.5rem; }
  .actions { flex-direction: column; }
  .btn { width: 100%; justify-content: center; }
  .record-header { flex-direction: column; align-items: flex-start; gap: 1rem; }
  .nav-tabs { overflow-x: auto; }
}
</style>
</head>
<body>

<canvas id="stars-canvas"></canvas>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<!-- AUTH OVERLAY -->
<!-- ══════════════════════════════════════════════════════════════════════════ -->
<div id="auth-overlay">
  <div class="auth-box">
    <h1 class="auth-title">Thought Record</h1>
    <p class="auth-subtitle">Your private CBT journal, synced to the cloud</p>

    <div class="auth-tabs">
      <button class="auth-tab active" onclick="switchAuthTab('login')">Sign In</button>
      <button class="auth-tab" onclick="switchAuthTab('signup')">Create Account</button>
    </div>

    <!-- LOGIN -->
    <div id="auth-login">
      <input class="auth-input" type="email" id="login-email" placeholder="Email address" autocomplete="email">
      <input class="auth-input" type="password" id="login-password" placeholder="Password" autocomplete="current-password">
      <button class="auth-btn" id="login-btn" onclick="handleLogin()">Sign In</button>
      <div class="auth-error" id="login-error"></div>
    </div>

    <!-- SIGNUP -->
    <div id="auth-signup" style="display:none;">
      <input class="auth-input" type="email" id="signup-email" placeholder="Email address" autocomplete="email">
      <input class="auth-input" type="password" id="signup-password" placeholder="Password (min 6 characters)" autocomplete="new-password">
      <button class="auth-btn" id="signup-btn" onclick="handleSignup()">Create Account</button>
      <div class="auth-error" id="signup-error"></div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════════════════════════════════════ -->
<!-- MAIN APP -->
<!-- ══════════════════════════════════════════════════════════════════════════ -->
<div id="app">
<div class="container">
  <div class="header">
    <h1 class="title">Thought Record</h1>
    <div class="user-bar">
      <span class="sync-indicator">
        <span class="sync-dot" id="sync-dot"></span>
        <span id="sync-label">Synced</span>
      </span>
      <span id="user-email" style="color:var(--muted); font-size:0.8rem;"></span>
      <button class="signout-btn" onclick="handleSignOut()">Sign out</button>
    </div>
  </div>

  <!-- NAVIGATION -->
  <div class="nav-tabs">
    <button class="nav-tab active" onclick="switchTab('new-record')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><path d="M12 5v14M5 12h14"/></svg>
      New Record
    </button>
    <button class="nav-tab" onclick="switchTab('history')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>
      History
    </button>
    <button class="nav-tab" onclick="switchTab('insights')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><line x1="12" y1="20" x2="12" y2="10"/><line x1="18" y1="20" x2="18" y2="4"/><line x1="6" y1="20" x2="6" y2="16"/></svg>
      Insights
    </button>
    <button class="nav-tab" onclick="switchTab('examples')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/><path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/></svg>
      Examples
    </button>
    <button class="nav-tab" onclick="switchTab('toolkit')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><rect x="3" y="3" width="18" height="18" rx="2" ry="2"/><line x1="9" y1="9" x2="15" y2="9"/><line x1="9" y1="15" x2="15" y2="15"/></svg>
      Toolkit
    </button>
  </div>

  <!-- TAB: NEW RECORD -->
  <div id="tab-new-record" class="tab-content active">
    <div class="card">
      <div class="section">
        <label class="section-label">Situation</label>
        <div class="helper-text">What happened? Where were you? Who was involved?</div>
        <textarea id="situation" placeholder="Describe the situation..."></textarea>
      </div>

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

      <div class="section">
        <label class="section-label">Automatic Thoughts</label>
        <div class="helper-text">What went through your mind?</div>
        <textarea id="thoughts" placeholder="What thoughts came up..."></textarea>
      </div>

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
        <div class="distortion-info-trigger" onclick="toggleDistortionInfo(this)">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><circle cx="12" cy="12" r="10"></circle><line x1="12" y1="16" x2="12" y2="12"></line><line x1="12" y1="8" x2="12.01" y2="8"></line></svg>
          <span>Learn about these patterns</span>
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><polyline points="6 9 12 15 18 9"></polyline></svg>
        </div>
        <div class="distortion-details" id="distortion-details">
          <div class="distortion-item"><div class="distortion-name">All-or-Nothing Thinking</div><div class="distortion-description">Viewing situations in only two categories instead of on a continuum. Things are either perfect or terrible, with nothing in between.</div><div class="distortion-example">"I'm wasting my time" — Reality: You tutor, created websites, learned French, go to therapy. Not everything has to be productive to have value.</div></div>
          <div class="distortion-item"><div class="distortion-name">Overgeneralization</div><div class="distortion-description">Making a broad conclusion based on a single incident. Using words like "always," "never," "everyone."</div><div class="distortion-example">"No matter how much I try, nothing works" — Reality: You CAN challenge thoughts now, use techniques like 54321 and box breathing.</div></div>
          <div class="distortion-item"><div class="distortion-name">Catastrophizing</div><div class="distortion-description">Expecting the worst possible outcome without evidence.</div><div class="distortion-example">"I will be all alone abroad" — Reality: You can't know that. You might find people who care.</div></div>
          <div class="distortion-item"><div class="distortion-name">Mind Reading</div><div class="distortion-description">Assuming you know what others are thinking without adequate evidence.</div><div class="distortion-example">"Uliana hates me" — Reality: She smiled, helped when sick, said she's not mad.</div></div>
          <div class="distortion-item"><div class="distortion-name">Fortune Telling</div><div class="distortion-description">Predicting the future negatively without realistic consideration of other outcomes.</div><div class="distortion-example">"Nothing will work out for me" — Reality: You never know unless you try.</div></div>
          <div class="distortion-item"><div class="distortion-name">Emotional Reasoning</div><div class="distortion-description">Believing something is true because you feel it strongly, ignoring evidence to the contrary.</div><div class="distortion-example">"I feel like all my achievements are worthless" — Reality: Your feelings are valid, but many people admire your achievements.</div></div>
          <div class="distortion-item"><div class="distortion-name">Should Statements</div><div class="distortion-description">Having fixed rules about how you or others should behave.</div><div class="distortion-example">"I should be able to handle everything without crying" — Reality: You're human, not a robot. Vulnerability isn't weakness.</div></div>
          <div class="distortion-item"><div class="distortion-name">Labeling</div><div class="distortion-description">Assigning global negative traits to yourself or others.</div><div class="distortion-example">"I'm weak" — Reality: You reached out for help, went to therapy despite fear, spoke up about homophobia. That's strength.</div></div>
          <div class="distortion-item"><div class="distortion-name">Personalization</div><div class="distortion-description">Blaming yourself for things outside your control.</div><div class="distortion-example">"They didn't respond, so what I said must not matter" — Reality: Silence is theirs, not yours.</div></div>
          <div class="distortion-item"><div class="distortion-name">Discounting the Positive</div><div class="distortion-description">Rejecting positive experiences by insisting they "don't count."</div><div class="distortion-example">"Everyone is better than me" — Reality: You have unique strengths: B2-C1 English self-taught, best at French in your group.</div></div>
        </div>
      </div>

      <div class="section">
        <label class="section-label">If a Friend Said This...</label>
        <div class="helper-text">What would you tell a friend in this situation?</div>
        <textarea id="friend-response" placeholder="How would you respond with compassion?"></textarea>
      </div>

      <div class="section">
        <label class="section-label">Balanced Conclusion</label>
        <div class="helper-text">What's a more balanced way to view this situation?</div>
        <div class="conclusion-box">
          <textarea id="conclusion" placeholder="A more compassionate, realistic perspective..."></textarea>
        </div>
      </div>

      <div class="actions">
        <button class="btn btn-primary" onclick="saveRecord()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:18px;height:18px;"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"></path><polyline points="17 21 17 13 7 13 7 21"></polyline><polyline points="7 3 7 8 15 8"></polyline></svg>
          Save to Cloud
        </button>
        <button class="btn btn-secondary" onclick="downloadCurrentPDF()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:18px;height:18px;"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"></path><polyline points="7 10 12 15 17 10"></polyline><line x1="12" y1="15" x2="12" y2="3"></line></svg>
          Download PDF
        </button>
        <button class="btn btn-secondary" onclick="clearForm()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:18px;height:18px;"><polyline points="3 6 5 6 21 6"></polyline><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path></svg>
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
      <div class="stats-grid">
        <div class="stat-card"><div class="stat-value" id="total-records">0</div><div class="stat-label">Total Records</div></div>
        <div class="stat-card"><div class="stat-value" id="avg-intensity">-</div><div class="stat-label">Avg Intensity</div></div>
        <div class="stat-card"><div class="stat-value" id="last-week">0</div><div class="stat-label">Past Week</div></div>
      </div>
      <div class="chart-container"><canvas id="intensityChart"></canvas></div>
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
      <div class="example-card" onclick="loadExample('alone-abroad')"><div class="example-thought">"I will be all alone abroad"</div><div class="example-response"><strong>Challenge:</strong> Is it a fact or a thought? → You can't know that. You might find people who will care.</div><span class="example-tag">Catastrophizing</span><span class="example-tag">Fortune Telling</span></div>
      <div class="example-card" onclick="loadExample('weak')"><div class="example-thought">"I'm weak"</div><div class="example-response"><strong>Evidence Against:</strong> I reached out to my friend. I decided to go to therapy despite fear. I spoke up about homophobia to my professor. I got up for an exam after a panic attack.</div><span class="example-tag">Labeling</span><span class="example-tag">Discounting the Positive</span></div>
      <div class="example-card" onclick="loadExample('unintelligent')"><div class="example-thought">"I'm unintelligent"</div><div class="example-response"><strong>Evidence Against:</strong> 200/200 English exam. B2-C1 English self-taught. Best at French in my group. Created research websites. 2+ years tutoring experience.</div><span class="example-tag">Labeling</span><span class="example-tag">All-or-Nothing</span></div>
      <div class="example-card" onclick="loadExample('uliana-hates')"><div class="example-thought">"Uliana hates me"</div><div class="example-response"><strong>Evidence Against:</strong> She smiled at me. She helped with the exam when she had a fever. She said "I'm not mad at you."</div><span class="example-tag">Mind Reading</span><span class="example-tag">Catastrophizing</span></div>
      <div class="example-card" onclick="loadExample('nothing-works')"><div class="example-thought">"No matter how much I try, nothing works"</div><div class="example-response"><strong>Evidence Against:</strong> I CAN challenge my thoughts now. I can use techniques: 54321, box breathing. I'm getting help with diagnosed disorders.</div><span class="example-tag">Overgeneralization</span><span class="example-tag">Discounting the Positive</span></div>
      <div class="example-card" onclick="loadExample('problems-not-real')"><div class="example-thought">"My pain isn't real"</div><div class="example-response"><strong>Reality:</strong> I have two diagnosed anxiety disorders. 7-8 panic attacks in 5 months. Pain can't be measured or compared. If it's real to me, it IS real.</div><span class="example-tag">Discounting the Positive</span><span class="example-tag">Emotional Reasoning</span></div>
      <div class="example-card" onclick="loadExample('nothing-matters')"><div class="example-thought">"Nothing I say matters"</div><div class="example-response"><strong>Alternative View:</strong> Your worth isn't tied to whether they responded. Silence stings, but the silence is theirs, not yours.</div><span class="example-tag">Personalization</span><span class="example-tag">All-or-Nothing</span></div>
      <div class="example-card" onclick="loadExample('comparison')"><div class="example-thought">"Everyone is better than me"</div><div class="example-response"><strong>Reality:</strong> People are different — apples, oranges, peaches. Comparison is pointless when each of us is so different.</div><span class="example-tag">Overgeneralization</span><span class="example-tag">Discounting the Positive</span></div>
    </div>
  </div>

  <!-- TAB: TOOLKIT -->
  <div id="tab-toolkit" class="tab-content">
    <div class="card">
      <label class="section-label">Quick Interventions</label>
      <div class="helper-text">Tools to use when feeling overwhelmed</div>
      <div class="toolkit-grid">
        <div class="toolkit-item"><div class="toolkit-title">54321 Grounding Technique</div><div class="toolkit-content"><ul class="toolkit-steps"><li>Name 5 things you can see</li><li>Name 4 things you can touch</li><li>Name 3 things you can hear</li><li>Name 2 things you can smell</li><li>Name 1 thing you can taste</li></ul><em style="color: var(--muted); font-size: 0.875rem;">Brings you back to the present moment</em></div></div>
        <div class="toolkit-item"><div class="toolkit-title">Box Breathing</div><div class="toolkit-content"><ul class="toolkit-steps"><li>Breathe in for 4 counts</li><li>Hold for 4 counts</li><li>Breathe out for 4 counts</li><li>Hold for 4 counts</li><li>Repeat 4-5 times</li></ul><em style="color: var(--muted); font-size: 0.875rem;">Calms the nervous system</em></div></div>
        <div class="toolkit-item"><div class="toolkit-title">Fact vs. Thought</div><div class="toolkit-content">Ask yourself: "Is this a fact or a thought?"<ul class="toolkit-steps"><li>Facts: Concrete, observable, provable</li><li>Thoughts: Interpretations, predictions, opinions</li><li>Most distressing things are thoughts, not facts</li></ul></div></div>
        <div class="toolkit-item"><div class="toolkit-title">The Friend Test</div><div class="toolkit-content">If a friend told you this about themselves, what would you say?<ul class="toolkit-steps"><li>We're often kinder to friends than ourselves</li><li>This exposes double standards</li><li>Helps find compassionate perspective</li></ul></div></div>
        <div class="toolkit-item"><div class="toolkit-title">Break It Down</div><div class="toolkit-content">When something feels too hard:<ul class="toolkit-steps"><li>Put on coat</li><li>Put on shoes</li><li>Go outside</li><li>Walk to the park</li><li>Listen to music</li></ul><em style="color: var(--muted); font-size: 0.875rem;">One tiny step at a time</em></div></div>
        <div class="toolkit-item"><div class="toolkit-title">Pain Is Valid</div><div class="toolkit-content">Pain can't be measured or compared:<ul class="toolkit-steps"><li>If it's real to you, it IS real</li><li>Your problems don't take care away from anyone</li><li>You wouldn't tell someone with headaches to "shut up because others have cancer"</li></ul></div></div>
      </div>
    </div>
  </div>
</div>
</div>

<div class="saved-msg" id="saved-msg">✓ Record saved</div>

<script>
// ══════════════════════════════════════════════════════════════════════════════
// STARFIELD
// ══════════════════════════════════════════════════════════════════════════════
const canvas = document.getElementById('stars-canvas');
const ctx = canvas.getContext('2d');
let stars = [];
function resizeCanvas() { canvas.width = window.innerWidth; canvas.height = window.innerHeight; initStars(); }
function initStars() { stars = []; const n = Math.floor((canvas.width * canvas.height) / 3000); for (let i = 0; i < n; i++) stars.push({ x: Math.random()*canvas.width, y: Math.random()*canvas.height, radius: Math.random()*1.5, opacity: Math.random()*0.5+0.3, twinkleSpeed: Math.random()*0.02+0.005 }); }
function drawStars() { ctx.clearRect(0,0,canvas.width,canvas.height); stars.forEach(s => { s.opacity += s.twinkleSpeed; if (s.opacity > 0.8 || s.opacity < 0.2) s.twinkleSpeed = -s.twinkleSpeed; ctx.beginPath(); ctx.arc(s.x,s.y,s.radius,0,Math.PI*2); ctx.fillStyle=`rgba(240,232,208,${s.opacity})`; ctx.fill(); }); requestAnimationFrame(drawStars); }
window.addEventListener('resize', resizeCanvas);
resizeCanvas(); drawStars();

// ══════════════════════════════════════════════════════════════════════════════
// AUTH UI
// ══════════════════════════════════════════════════════════════════════════════
function switchAuthTab(tab) {
  document.querySelectorAll('.auth-tab').forEach(t => t.classList.remove('active'));
  event.target.classList.add('active');
  document.getElementById('auth-login').style.display = tab === 'login' ? 'block' : 'none';
  document.getElementById('auth-signup').style.display = tab === 'signup' ? 'block' : 'none';
}

async function handleLogin() {
  const email = document.getElementById('login-email').value.trim();
  const password = document.getElementById('login-password').value;
  const btn = document.getElementById('login-btn');
  const errorEl = document.getElementById('login-error');
  errorEl.textContent = '';
  if (!email || !password) { errorEl.textContent = 'Please fill in all fields.'; return; }
  btn.disabled = true; btn.textContent = 'Signing in...';
  try {
    await FirebaseREST.signIn(email, password);
  } catch(e) {
    errorEl.textContent = friendlyAuthError(e.message);
    btn.disabled = false; btn.textContent = 'Sign In';
  }
}

async function handleSignup() {
  const email = document.getElementById('signup-email').value.trim();
  const password = document.getElementById('signup-password').value;
  const btn = document.getElementById('signup-btn');
  const errorEl = document.getElementById('signup-error');
  errorEl.textContent = '';
  if (!email || !password) { errorEl.textContent = 'Please fill in all fields.'; return; }
  if (password.length < 6) { errorEl.textContent = 'Password must be at least 6 characters.'; return; }
  btn.disabled = true; btn.textContent = 'Creating account...';
  try {
    await FirebaseREST.signUp(email, password);
  } catch(e) {
    errorEl.textContent = friendlyAuthError(e.message);
    btn.disabled = false; btn.textContent = 'Create Account';
  }
}

function friendlyAuthError(msg) {
  if (msg.includes('EMAIL_EXISTS')) return 'An account with this email already exists.';
  if (msg.includes('INVALID_PASSWORD') || msg.includes('INVALID_LOGIN_CREDENTIALS')) return 'Incorrect email or password.';
  if (msg.includes('USER_NOT_FOUND')) return 'No account found with this email.';
  if (msg.includes('TOO_MANY_ATTEMPTS')) return 'Too many attempts. Please try again later.';
  if (msg.includes('WEAK_PASSWORD')) return 'Password must be at least 6 characters.';
  if (msg.includes('INVALID_EMAIL')) return 'Please enter a valid email address.';
  return msg;
}

async function handleSignOut() {
  await FirebaseREST.signOut();
  cachedRecords = [];
}

// ══════════════════════════════════════════════════════════════════════════════
// CLOUD SYNC — Firestore
// ══════════════════════════════════════════════════════════════════════════════
let cachedRecords = [];

function setSyncStatus(status) {
  const dot = document.getElementById('sync-dot');
  const label = document.getElementById('sync-label');
  dot.className = 'sync-dot';
  if (status === 'syncing') { dot.classList.add('syncing'); label.textContent = 'Saving...'; }
  else if (status === 'error') { dot.classList.add('error'); label.textContent = 'Sync failed'; }
  else { label.textContent = 'Synced'; }
}

async function loadRecordsFromCloud() {
  try {
    setSyncStatus('syncing');
    const uid = FirebaseREST.currentUser.uid;
    const data = await FirebaseREST.getDocument('thoughtRecords', uid);
    if (data && data.recordsJSON) {
      cachedRecords = JSON.parse(data.recordsJSON);
    } else {
      cachedRecords = [];
    }
    setSyncStatus('synced');
  } catch(e) {
    console.error('Load failed:', e);
    setSyncStatus('error');
    cachedRecords = [];
  }
}

async function saveRecordsToCloud() {
  try {
    setSyncStatus('syncing');
    const uid = FirebaseREST.currentUser.uid;
    await FirebaseREST.setDocument('thoughtRecords', uid, {
      recordsJSON: JSON.stringify(cachedRecords),
      updatedAt: new Date().toISOString()
    });
    setSyncStatus('synced');
  } catch(e) {
    console.error('Save failed:', e);
    setSyncStatus('error');
    throw e;
  }
}

// ══════════════════════════════════════════════════════════════════════════════
// TAB SWITCHING
// ══════════════════════════════════════════════════════════════════════════════
function switchTab(tabName) {
  document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
  document.getElementById(`tab-${tabName}`).classList.add('active');
  event.target.closest('.nav-tab').classList.add('active');
  if (tabName === 'history') renderHistory();
  else if (tabName === 'insights') renderInsights();
}

// ══════════════════════════════════════════════════════════════════════════════
// INTENSITY SLIDER
// ══════════════════════════════════════════════════════════════════════════════
document.getElementById('intensity').addEventListener('input', (e) => {
  document.getElementById('intensity-value').textContent = e.target.value;
});

// ══════════════════════════════════════════════════════════════════════════════
// COGNITIVE DISTORTIONS TOGGLE
// ══════════════════════════════════════════════════════════════════════════════
function toggleDistortion(el) { el.classList.toggle('selected'); }
function toggleDistortionInfo(trigger) {
  trigger.classList.toggle('expanded');
  document.getElementById('distortion-details').classList.toggle('expanded');
}

// ══════════════════════════════════════════════════════════════════════════════
// EXAMPLES
// ══════════════════════════════════════════════════════════════════════════════
const examples = {
  'alone-abroad': { thoughts: "I will be all alone abroad. Nobody will care about me when I am abroad.", evidenceFor: "", evidenceAgainst: "I can't know that for certain. I might find people who will care. It's possible to build new connections.", friendResponse: "You can't predict the future with certainty. Many people move abroad and find meaningful connections.", conclusion: "It's a thought, not a fact. I can't know what will happen until I try.", distortions: ['Catastrophizing', 'Fortune Telling'] },
  'weak': { thoughts: "I'm weak", evidenceFor: "I cry. I have panic attacks.", evidenceAgainst: "I reached out to my friend. I made the decision to go to therapy even though I was terrified. I spoke up about homophobia to my professor. I spent the entire night in a mental breakdown, still woke up for an exam.", friendResponse: "You're human, not a robot. Softness and vulnerability aren't weaknesses. Those actions required immense courage.", conclusion: "I am not weak. I'm dealing with difficult circumstances and still showing up.", distortions: ['Labeling', 'Discounting the Positive'] },
  'unintelligent': { thoughts: "I'm unintelligent", evidenceFor: "I can't come up with creative ideas in class.", evidenceAgainst: "200/200 English exam. B2-C1 English self-taught in one year. Best at French in my group. Created research websites. 2+ years tutoring experience.", friendResponse: "Mental health issues aren't solved through intelligence alone. Your academic achievements clearly demonstrate your intelligence.", conclusion: "I have strong evidence of my intelligence. Mental health struggles don't reflect on intelligence.", distortions: ['Labeling', 'All-or-Nothing'] },
  'uliana-hates': { thoughts: "Uliana hates me", evidenceFor: "I hurt her by ghosting her for 4 days.", evidenceAgainst: "She smiled at me in class. She helped me with the exam when she had a fever. She said 'I am not mad at you.' We talked after class and text each other about normal things.", friendResponse: "Actions speak louder than one difficult moment. She's continuing to engage with you, help you, spend time with you. That shows care, not hate.", conclusion: "Her current actions show she doesn't hate me — she's processing what happened while still maintaining our friendship.", distortions: ['Mind Reading', 'Catastrophizing'] },
  'nothing-works': { thoughts: "No matter how much I try, nothing works", evidenceFor: "I still have panic attacks. I still cry.", evidenceAgainst: "I can challenge my thoughts now (progress). I can use techniques: 54321, box breathing, thought/fact testing. I have an easier time talking to people than a year ago.", friendResponse: "Recovery isn't linear. You're building skills that will compound over time.", conclusion: "Progress is happening even if I can't see it clearly in the moment. I have more tools than I did before.", distortions: ['Overgeneralization', 'Discounting the Positive'] },
  'problems-not-real': { thoughts: "My pain isn't real. I don't have any real problems.", evidenceFor: "Some people have experienced abuse, financial problems, war.", evidenceAgainst: "I have two diagnosed anxiety disorders: SAD and GAD. I have had 7-8 panic attacks over the past 5 months. I am gay in a homophobic country.", friendResponse: "Pain isn't something that can be measured. If it is real to you and it causes you pain, then it is real.", conclusion: "Pain can't be compared. My diagnosed disorders and experiences are valid and deserve treatment.", distortions: ['Discounting the Positive', 'Emotional Reasoning'] },
  'nothing-matters': { thoughts: "Nothing I say matters", evidenceFor: "They didn't respond to my message about conversion therapy.", evidenceAgainst: "The teacher responded, disagreed, but let me post the links. No retaliation, no judgement.", friendResponse: "Your worth isn't tied to whether they responded. You did the thing you were terrified to do.", conclusion: "Not everyone will respond to what matters deeply to me. That doesn't make it meaningless. Silence stings, but the silence is theirs, not mine.", distortions: ['Personalization', 'All-or-Nothing'] },
  'comparison': { thoughts: "Everyone is better than me", evidenceFor: "People seem more confident, successful, happy.", evidenceAgainst: "People are different: some are apples, some are oranges. I have B2-C1 English (self-taught), best at French in my group, 200/200 on exams.", friendResponse: "Comparison is pointless when each of us is so different. You're measuring yourself against a highlight reel.", conclusion: "Comparison steals joy and isn't accurate. I have my own strengths and journey.", distortions: ['Overgeneralization', 'Discounting the Positive'] }
};

function loadExample(key) {
  const ex = examples[key];
  if (!ex) return;
  switchTab('new-record');
  // Call switchTab needs event — workaround:
  document.querySelectorAll('.tab-content').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
  document.getElementById('tab-new-record').classList.add('active');
  document.querySelector('.nav-tab').classList.add('active');
  document.getElementById('thoughts').value = ex.thoughts;
  document.getElementById('evidence-for').value = ex.evidenceFor;
  document.getElementById('evidence-against').value = ex.evidenceAgainst;
  document.getElementById('friend-response').value = ex.friendResponse;
  document.getElementById('conclusion').value = ex.conclusion;
  document.querySelectorAll('.distortion-tag').forEach(tag => {
    tag.classList.remove('selected');
    if (ex.distortions.includes(tag.textContent)) tag.classList.add('selected');
  });
  window.scrollTo({ top: 0, behavior: 'smooth' });
  showMsg('✓ Example loaded', false);
}

// ══════════════════════════════════════════════════════════════════════════════
// SAVE RECORD
// ══════════════════════════════════════════════════════════════════════════════
async function saveRecord() {
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

  cachedRecords.push(record);
  try {
    await saveRecordsToCloud();
    showMsg('✓ Saved to cloud', false);
    setTimeout(clearForm, 400);
  } catch(e) {
    cachedRecords.pop(); // rollback
    showMsg('✗ Save failed', true);
  }
}

// ══════════════════════════════════════════════════════════════════════════════
// DOWNLOAD PDF
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

function generatePDF(record, date) {
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();
  const pageWidth = doc.internal.pageSize.getWidth();
  const margin = 20;
  const maxWidth = pageWidth - 2 * margin;
  let y = 20;
  doc.setFontSize(20); doc.setTextColor(106, 90, 205); doc.text('Thought Record', margin, y); y += 10;
  doc.setFontSize(10); doc.setTextColor(150, 150, 150); doc.text(new Date(date).toLocaleString(), margin, y); y += 15;
  const addSection = (label, content) => {
    if (y > 270) { doc.addPage(); y = 20; }
    doc.setFontSize(12); doc.setTextColor(106, 90, 205); doc.text(label, margin, y); y += 7;
    doc.setFontSize(10);
    if (content) { doc.setTextColor(0,0,0); const lines = doc.splitTextToSize(content, maxWidth); doc.text(lines, margin, y); y += lines.length * 5 + 10; }
    else { doc.setTextColor(150,150,150); doc.text('(not filled)', margin, y); y += 12; }
  };
  addSection('Situation', record.situation);
  addSection('Emotions', record.emotions ? `${record.emotions} (${record.intensity}/10)` : '');
  addSection('Automatic Thoughts', record.thoughts);
  addSection('Evidence For', record.evidenceFor);
  addSection('Evidence Against', record.evidenceAgainst);
  addSection('Cognitive Distortions', record.distortions ? record.distortions.join(', ') : '');
  addSection('If a Friend Said This...', record.friendResponse);
  addSection('Balanced Conclusion', record.conclusion);
  doc.save(`thought-record-${new Date(date).toISOString().split('T')[0]}.pdf`);
}

// ══════════════════════════════════════════════════════════════════════════════
// RENDER HISTORY
// ══════════════════════════════════════════════════════════════════════════════
function renderHistory() {
  const container = document.getElementById('records-container');
  if (cachedRecords.length === 0) { container.innerHTML = '<div class="no-records">No records yet. Save your first thought record!</div>'; return; }
  const sorted = [...cachedRecords].reverse();
  container.innerHTML = sorted.map((record, i) => {
    const realIndex = cachedRecords.length - 1 - i;
    const d = new Date(record.timestamp);
    const dateStr = d.toLocaleDateString('en-US', { weekday:'long', year:'numeric', month:'long', day:'numeric' }) + ' · ' + d.toLocaleTimeString('en-US', { hour:'2-digit', minute:'2-digit' });
    return `
      <div class="record-card" id="record-${realIndex}">
        <div class="record-header">
          <div class="record-date">${dateStr}</div>
          <div class="record-actions">
            <button class="icon-btn" onclick="editRecord(${realIndex})"><svg viewBox="0 0 24 24"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>Edit</button>
            <button class="icon-btn" onclick="downloadRecordPDF(${realIndex})"><svg viewBox="0 0 24 24"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>PDF</button>
            <button class="icon-btn icon-btn-delete" onclick="deleteRecord(${realIndex})"><svg viewBox="0 0 24 24"><polyline points="3 6 5 6 21 6"/><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"/></svg>Delete</button>
          </div>
        </div>
        <div class="record-content" id="record-content-${realIndex}">
          ${record.situation ? `<div class="record-field"><div class="record-field-label">Situation</div><div class="record-field-value">${record.situation}</div></div>` : ''}
          ${record.emotions ? `<div class="record-field"><div class="record-field-label">Emotions</div><div class="record-field-value">${record.emotions} · ${record.intensity}/10</div></div>` : ''}
          ${record.thoughts ? `<div class="record-field"><div class="record-field-label">Automatic Thoughts</div><div class="record-field-value">${record.thoughts}</div></div>` : ''}
          ${record.conclusion ? `<div class="record-field"><div class="record-field-label">Balanced Conclusion</div><div class="record-field-value"><strong>${record.conclusion}</strong></div></div>` : ''}
          ${record.distortions && record.distortions.length > 0 ? `<div class="record-field"><div class="record-field-label">Cognitive Distortions</div><div class="record-distortions">${record.distortions.map(d=>`<span class="record-distortion-tag">${d}</span>`).join('')}</div></div>` : ''}
        </div>
        <div class="edit-form" id="edit-form-${realIndex}">
          <label class="section-label" style="font-size: 1rem;">Edit Record</label>
          <textarea id="edit-situation-${realIndex}" placeholder="Situation">${record.situation || ''}</textarea>
          <textarea id="edit-emotions-${realIndex}" placeholder="Emotions">${record.emotions || ''}</textarea>
          <input type="number" id="edit-intensity-${realIndex}" min="1" max="10" value="${record.intensity || 5}" style="width:100px; margin-bottom:0.75rem; background:rgba(255,255,255,0.04); border:1px solid var(--card-border); border-radius:8px; padding:0.5rem; color:var(--text);">
          <textarea id="edit-thoughts-${realIndex}" placeholder="Automatic Thoughts">${record.thoughts || ''}</textarea>
          <textarea id="edit-evidence-for-${realIndex}" placeholder="Evidence For">${record.evidenceFor || ''}</textarea>
          <textarea id="edit-evidence-against-${realIndex}" placeholder="Evidence Against">${record.evidenceAgainst || ''}</textarea>
          <textarea id="edit-friend-response-${realIndex}" placeholder="If a Friend Said This...">${record.friendResponse || ''}</textarea>
          <textarea id="edit-conclusion-${realIndex}" placeholder="Balanced Conclusion">${record.conclusion || ''}</textarea>
          <div class="edit-actions">
            <button class="icon-btn" onclick="saveEdit(${realIndex})" style="background:var(--lavender);color:var(--night);"><svg viewBox="0 0 24 24"><polyline points="20 6 9 17 4 12"></polyline></svg>Save Changes</button>
            <button class="icon-btn" onclick="cancelEdit(${realIndex})"><svg viewBox="0 0 24 24"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>Cancel</button>
          </div>
        </div>
      </div>`;
  }).join('');
}

// ══════════════════════════════════════════════════════════════════════════════
// EDIT / SAVE / DELETE RECORDS
// ══════════════════════════════════════════════════════════════════════════════
function editRecord(index) {
  document.getElementById(`record-${index}`).classList.add('edit-mode');
  document.getElementById(`edit-form-${index}`).classList.add('active');
  document.getElementById(`record-content-${index}`).style.display = 'none';
}
function cancelEdit(index) {
  document.getElementById(`record-${index}`).classList.remove('edit-mode');
  document.getElementById(`edit-form-${index}`).classList.remove('active');
  document.getElementById(`record-content-${index}`).style.display = 'grid';
}

async function saveEdit(index) {
  const prev = { ...cachedRecords[index] };
  cachedRecords[index] = {
    ...cachedRecords[index],
    situation: document.getElementById(`edit-situation-${index}`).value,
    emotions: document.getElementById(`edit-emotions-${index}`).value,
    intensity: document.getElementById(`edit-intensity-${index}`).value,
    thoughts: document.getElementById(`edit-thoughts-${index}`).value,
    evidenceFor: document.getElementById(`edit-evidence-for-${index}`).value,
    evidenceAgainst: document.getElementById(`edit-evidence-against-${index}`).value,
    friendResponse: document.getElementById(`edit-friend-response-${index}`).value,
    conclusion: document.getElementById(`edit-conclusion-${index}`).value
  };
  try {
    await saveRecordsToCloud();
    showMsg('✓ Changes saved', false);
    renderHistory();
  } catch(e) {
    cachedRecords[index] = prev;
    showMsg('✗ Save failed', true);
  }
}

async function deleteRecord(index) {
  if (!confirm('Delete this record? This cannot be undone.')) return;
  const removed = cachedRecords.splice(index, 1);
  try {
    await saveRecordsToCloud();
    renderHistory();
    renderInsights();
  } catch(e) {
    cachedRecords.splice(index, 0, removed[0]);
    showMsg('✗ Delete failed', true);
  }
}

function downloadRecordPDF(index) {
  const record = cachedRecords[index];
  if (record) generatePDF(record, record.timestamp);
}

// ══════════════════════════════════════════════════════════════════════════════
// INSIGHTS
// ══════════════════════════════════════════════════════════════════════════════
let intensityChart = null;
function renderInsights() {
  if (cachedRecords.length === 0) {
    document.getElementById('total-records').textContent = '0';
    document.getElementById('avg-intensity').textContent = '-';
    document.getElementById('last-week').textContent = '0';
    document.getElementById('pattern-list').innerHTML = '<div class="no-records">No data yet</div>';
    return;
  }
  const intensities = cachedRecords.map(r => parseInt(r.intensity) || 5);
  document.getElementById('total-records').textContent = cachedRecords.length;
  document.getElementById('avg-intensity').textContent = (intensities.reduce((a,b) => a+b, 0) / intensities.length).toFixed(1);
  const weekAgo = new Date(); weekAgo.setDate(weekAgo.getDate() - 7);
  document.getElementById('last-week').textContent = cachedRecords.filter(r => new Date(r.timestamp) > weekAgo).length;
  renderIntensityChart();
  renderPatterns();
}

function renderIntensityChart() {
  const ctx2 = document.getElementById('intensityChart');
  if (!ctx2) return;
  if (intensityChart) intensityChart.destroy();
  const recent = cachedRecords.slice(-10);
  intensityChart = new Chart(ctx2, {
    type: 'line',
    data: { labels: recent.map((_,i) => `#${cachedRecords.length-recent.length+i+1}`), datasets: [{ label: 'Intensity', data: recent.map(r => parseInt(r.intensity)||5), borderColor: '#c9b8e8', backgroundColor: 'rgba(201,184,232,0.1)', tension: 0.4, fill: true }] },
    options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } }, scales: { y: { min:1, max:10, ticks: { color:'#e8e0f0', stepSize:1 }, grid: { color:'rgba(255,255,255,0.08)' } }, x: { ticks: { color:'#e8e0f0' }, grid: { color:'rgba(255,255,255,0.08)' } } } }
  });
}

function renderPatterns() {
  const counts = {};
  cachedRecords.forEach(r => { if (r.distortions) r.distortions.forEach(d => { counts[d] = (counts[d]||0)+1; }); });
  const sorted = Object.entries(counts).sort((a,b) => b[1]-a[1]).slice(0,5);
  document.getElementById('pattern-list').innerHTML = sorted.length === 0
    ? '<div class="no-records">No patterns identified yet</div>'
    : sorted.map(([name, count]) => `<div class="pattern-item"><div class="pattern-name">${name}</div><div class="pattern-count">${count}</div></div>`).join('');
}

// ══════════════════════════════════════════════════════════════════════════════
// CLEAR FORM
// ══════════════════════════════════════════════════════════════════════════════
function clearForm() {
  ['situation','emotions','thoughts','evidence-for','evidence-against','friend-response','conclusion'].forEach(id => { const el = document.getElementById(id); if(el) el.value = ''; });
  document.getElementById('intensity').value = 5;
  document.getElementById('intensity-value').textContent = 5;
  document.querySelectorAll('.distortion-tag.selected').forEach(t => t.classList.remove('selected'));
}

// ══════════════════════════════════════════════════════════════════════════════
// SHOW MESSAGE
// ══════════════════════════════════════════════════════════════════════════════
function showMsg(text, isError) {
  const msg = document.getElementById('saved-msg');
  msg.textContent = text;
  msg.className = 'saved-msg' + (isError ? ' error' : '');
  msg.classList.add('show');
  setTimeout(() => msg.classList.remove('show'), 3000);
}

// Enter key on auth inputs
document.getElementById('login-password').addEventListener('keydown', e => { if(e.key==='Enter') handleLogin(); });
document.getElementById('signup-password').addEventListener('keydown', e => { if(e.key==='Enter') handleSignup(); });
</script>

</body>
</html>
