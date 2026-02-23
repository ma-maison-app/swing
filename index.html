<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Thought Record · CBT Worksheet</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Work+Sans:wght@300;400;500;600;700&family=Allura&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<script>
// ══════════════════════════════════════════════════════════════════════════════
// SUPABASE REST API — No SDK needed
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
    const url = `${this.config.url}/auth/v1/signup`;
    const response = await fetch(url, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', 'apikey': this.config.anonKey },
      body: JSON.stringify({ email, password })
    });
    const data = await response.json();
    if (data.error || data.msg) throw new Error(data.error_description || data.msg || data.error);
    if (!data.access_token) throw new Error('Check your email to confirm your account before signing in.');
    this.currentUser = { uid: data.user.id, email: data.user.email, token: data.access_token, refreshToken: data.refresh_token };
    await this.storeUser(this.currentUser);
    if (window._authCallback) window._authCallback(this.currentUser);
    return this.currentUser;
  },

  signIn: async function(email, password) {
    const url = `${this.config.url}/auth/v1/token?grant_type=password`;
    const response = await fetch(url, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', 'apikey': this.config.anonKey },
      body: JSON.stringify({ email, password })
    });
    const data = await response.json();
    if (data.error || data.error_description) throw new Error(data.error_description || data.error);
    this.currentUser = { uid: data.user.id, email: data.user.email, token: data.access_token, refreshToken: data.refresh_token };
    await this.storeUser(this.currentUser);
    if (window._authCallback) window._authCallback(this.currentUser);
    return this.currentUser;
  },

  signOut: async function() {
    if (this.currentUser) {
      try {
        await fetch(`${this.config.url}/auth/v1/logout`, {
          method: 'POST',
          headers: { 'apikey': this.config.anonKey, 'Authorization': `Bearer ${this.currentUser.token}` }
        });
      } catch(e) {}
    }
    this.currentUser = null;
    this._memoryStore = {};
    try { const db = await this._getDB(); const t = db.transaction([this._storeName], 'readwrite'); t.objectStore(this._storeName).delete('supabase_user'); } catch(e) {}
    try { sessionStorage.removeItem('supabase_user'); } catch(e) {}
    if (window._authCallback) window._authCallback(null);
  },

  setDocument: async function(collection, docId, data) {
    if (!this.currentUser) throw new Error('Not authenticated');
    await this.refreshTokenIfNeeded();
    const url = `${this.config.url}/rest/v1/${collection}?on_conflict=user_id`;
    const response = await fetch(url, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'apikey': this.config.anonKey,
        'Authorization': `Bearer ${this.currentUser.token}`,
        'Prefer': 'return=minimal,resolution=merge-duplicates'
      },
      body: JSON.stringify({ user_id: docId, ...this._flattenForSupabase(data) })
    });
    if (!response.ok) {
      let errText = '';
      try { const err = await response.json(); errText = err.message || err.hint || JSON.stringify(err); } catch(e) { errText = response.statusText; }
      throw new Error(errText);
    }
    return true;
  },

  getDocument: async function(collection, docId) {
    if (!this.currentUser) throw new Error('Not authenticated');
    await this.refreshTokenIfNeeded();
    const url = `${this.config.url}/rest/v1/${collection}?user_id=eq.${docId}&select=*`;
    const response = await fetch(url, {
      headers: { 'apikey': this.config.anonKey, 'Authorization': `Bearer ${this.currentUser.token}` }
    });
    const result = await response.json();
    if (!response.ok) throw new Error(result.message || JSON.stringify(result));
    if (!result || result.length === 0) return null;
    return this._unflattenFromSupabase(result[0]);
  },

  _flattenForSupabase: function(data) {
    // Convert camelCase keys to snake_case for Supabase
    const out = {};
    for (const [k, v] of Object.entries(data)) {
      const key = k.replace(/([A-Z])/g, '_$1').toLowerCase();
      out[key] = v;
    }
    return out;
  },

  _unflattenFromSupabase: function(row) {
    // Convert snake_case keys back to camelCase
    const out = {};
    for (const [k, v] of Object.entries(row)) {
      const key = k.replace(/_([a-z])/g, (_, c) => c.toUpperCase());
      out[key] = v;
    }
    return out;
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
    this._memoryStore.supabase_user = userData;
    try {
      const db = await this._getDB();
      const t = db.transaction([this._storeName], 'readwrite');
      t.objectStore(this._storeName).put(userData, 'supabase_user');
    } catch(e) {
      try { sessionStorage.setItem('supabase_user', JSON.stringify(userData)); } catch(e2) {}
    }
  },

  getStoredUser: async function() {
    if (this._memoryStore.supabase_user) {
      const u = this._memoryStore.supabase_user;
      if (Date.now() - u.timestamp < 60 * 60 * 1000) return u;
    }
    try {
      const db = await this._getDB();
      const t = db.transaction([this._storeName], 'readonly');
      const request = t.objectStore(this._storeName).get('supabase_user');
      const user = await new Promise((res, rej) => { request.onsuccess = () => res(request.result); request.onerror = () => rej(request.error); });
      if (user && Date.now() - user.timestamp < 60 * 60 * 1000) { this._memoryStore.supabase_user = user; return user; }
    } catch(e) {}
    try {
      const stored = sessionStorage.getItem('supabase_user');
      if (stored) { const user = JSON.parse(stored); if (Date.now() - user.timestamp < 60 * 60 * 1000) { this._memoryStore.supabase_user = user; return user; } }
    } catch(e) {}
    return null;
  },

  refreshTokenIfNeeded: async function() {
    if (!this.currentUser) return;
    const stored = this._memoryStore.supabase_user;
    if (!stored || Date.now() - stored.timestamp < 50 * 60 * 1000) return;
    const url = `${this.config.url}/auth/v1/token?grant_type=refresh_token`;
    const response = await fetch(url, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', 'apikey': this.config.anonKey },
      body: JSON.stringify({ refresh_token: this.currentUser.refreshToken })
    });
    const data = await response.json();
    if (data.error) { await this.signOut(); throw new Error('Session expired'); }
    this.currentUser.token = data.access_token;
    this.currentUser.refreshToken = data.refresh_token;
    await this.storeUser(this.currentUser);
  }
};

// ══════════════════════════════════════════════════════════════════════════════
// 🔧 YOUR SUPABASE CONFIG
// ══════════════════════════════════════════════════════════════════════════════
const firebaseConfig = {
  url: "https://zqkmxlzyuaiaynzdftec.supabase.co",
  anonKey: "sb_publishable_FvEg7rSQePiFDN7rnwfsiw_lZB7pgSV",
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
body { font-family: 'Work Sans', sans-serif; background: var(--night); color: var(--text); min-height: 100vh; overflow-x: hidden; padding: 2rem 1rem; }
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
  font-family: 'Work Sans', sans-serif; font-size: 0.95rem; font-weight: 500;
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
  font-family: 'Work Sans', sans-serif;
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
  padding: 0.9rem; font-family: 'Work Sans', sans-serif;
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
  font-family: 'Work Sans', sans-serif;
  transition: all 0.2s;
}
.signout-btn:hover { border-color: var(--blush); color: var(--blush); }

/* ── NAVIGATION TABS ── */
.nav-tabs { display: flex; gap: 0.5rem; margin-bottom: 2rem; border-bottom: 1px solid var(--card-border); flex-wrap: wrap; }
.nav-tab { background: none; border: none; color: var(--muted); font-family: 'Work Sans', sans-serif; font-size: 0.95rem; font-weight: 500; padding: 0.75rem 1.25rem; cursor: pointer; border-bottom: 2px solid transparent; transition: all 0.3s ease; display: flex; align-items: center; gap: 0.5rem; }
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
.section-label { font-family: 'Cormorant Garamond', serif; font-size: 1.5rem; font-weight: 600; color: var(--lavender); margin-bottom: 0.75rem; display: block; letter-spacing: 0.3px; }
.helper-text { font-size: 0.875rem; color: var(--muted); margin-bottom: 0.5rem; font-style: italic; }

/* ── INPUTS ── */
textarea, input[type="text"] { width: 100%; background: rgba(255,255,255,0.02); border: 1px solid var(--card-border); border-radius: 12px; padding: 1rem; color: var(--text); font-family: 'Work Sans', sans-serif; font-size: 1rem; line-height: 1.6; resize: vertical; transition: border-color 0.3s ease; }
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
.evidence-title { font-family: 'Cormorant Garamond', serif; font-size: 1.2rem; font-weight: 600; color: var(--blush); margin-bottom: 0.75rem; }
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
.btn { padding: 1rem 2rem; border-radius: 12px; border: none; font-family: 'Work Sans', sans-serif; font-size: 1rem; font-weight: 500; cursor: pointer; transition: all 0.3s ease; display: inline-flex; align-items: center; gap: 0.5rem; }
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


/* ── EMOTION PICKER ── */
.emotion-picker { margin-top: 0.75rem; }
.emotion-category { margin-bottom: 0.75rem; }
.emotion-category-label { font-size: 0.75rem; color: var(--muted); text-transform: uppercase; letter-spacing: 0.08em; margin-bottom: 0.4rem; display: block; }
.emotion-chips { display: flex; flex-wrap: wrap; gap: 0.4rem; }
.emotion-chip { background: rgba(255,255,255,0.04); border: 1px solid var(--card-border); color: var(--text); padding: 0.35rem 0.8rem; border-radius: 16px; font-size: 0.82rem; cursor: pointer; transition: all 0.2s ease; }
.emotion-chip:hover { border-color: var(--lavender); color: var(--lavender); background: rgba(201,184,232,0.1); }
.emotion-chip.selected { background: var(--lavender); color: var(--night); border-color: var(--lavender); }
.emotion-picker-toggle { font-size: 0.82rem; color: var(--muted); cursor: pointer; display: inline-flex; align-items: center; gap: 0.3rem; margin-bottom: 0.5rem; padding: 0.3rem 0; border: none; background: none; font-family: inherit; }
.emotion-picker-toggle:hover { color: var(--lavender); }
.emotion-picker-body { display: none; }
.emotion-picker-body.open { display: block; }
/* ── RESPONSIVE ── */
@media (max-width: 600px) {
  .title { font-size: 2.5rem; }
  .actions { flex-direction: column; }
  .btn { width: 100%; justify-content: center; }
  .record-header { flex-direction: column; align-items: flex-start; gap: 1rem; }
  .nav-tabs { overflow-x: auto; }
}

/* ── ACTIVITY LOG ── */
.al-category-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 0.75rem; margin-top: 0.5rem; }
@media (max-width: 600px) { .al-category-grid { grid-template-columns: 1fr; } }
.al-cat-btn {
  background: rgba(255,255,255,0.02); border: 1px solid var(--card-border);
  border-radius: 12px; padding: 1rem; cursor: pointer; transition: all 0.2s ease;
  display: flex; flex-direction: column; gap: 0.25rem;
}
.al-cat-btn:hover { border-color: var(--lavender); background: rgba(201,184,232,0.05); }
.al-cat-btn.active { background: rgba(201,184,232,0.12); border-color: var(--lavender); }
.al-cat-icon { font-size: 1.3rem; }
.al-cat-name { font-family: 'Cormorant Garamond', serif; font-size: 1.1rem; font-weight: 600; color: var(--lavender); }
.al-cat-desc { font-size: 0.8rem; color: var(--muted); }

.al-ratings { display: flex; flex-direction: column; gap: 1.25rem; margin-top: 0.5rem; }
.al-rating-row { display: flex; align-items: center; gap: 1rem; }
.al-rating-label { min-width: 130px; display: flex; flex-direction: column; gap: 0.2rem; }
.al-rating-hint { font-size: 0.75rem; color: var(--muted); }
.al-rating-control { flex: 1; display: flex; align-items: center; gap: 0.75rem; }
.al-range { flex: 1; }
.al-rating-val { font-family: 'Cormorant Garamond', serif; font-size: 1.4rem; font-weight: 600; color: var(--lavender); min-width: 28px; text-align: right; }
@media (max-width: 600px) { .al-rating-row { flex-direction: column; align-items: flex-start; } .al-rating-control { width: 100%; } }

.al-entry-card {
  background: rgba(255,255,255,0.02); border: 1px solid var(--card-border);
  border-radius: 12px; padding: 1.25rem; margin-bottom: 0.75rem; transition: all 0.2s;
}
.al-entry-card:hover { border-color: rgba(201,184,232,0.3); }
.al-entry-header { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 0.75rem; }
.al-entry-activity { font-family: 'Cormorant Garamond', serif; font-size: 1.15rem; color: var(--text); font-style: italic; }
.al-entry-meta { display: flex; align-items: center; gap: 0.5rem; flex-shrink: 0; }
.al-cat-pill {
  padding: 0.25rem 0.7rem; border-radius: 20px; font-size: 0.75rem; font-weight: 500;
}
.al-cat-pill.routine { background: rgba(201,184,232,0.15); color: var(--lavender); }
.al-cat-pill.necessary { background: rgba(232,200,212,0.15); color: var(--blush); }
.al-cat-pill.pleasure { background: rgba(212,169,106,0.15); color: var(--gold); }
.al-cat-pill.achievement { background: rgba(110,231,183,0.15); color: #6ee7b7; }
.al-entry-date { font-size: 0.78rem; color: var(--muted); }
.al-bars { display: flex; gap: 1rem; flex-wrap: wrap; }
.al-bar-group { display: flex; flex-direction: column; gap: 0.3rem; }
.al-bar-label { font-size: 0.72rem; color: var(--muted); text-transform: uppercase; letter-spacing: 0.05em; }
.al-bar-track { display: flex; gap: 2px; }
.al-bar-seg { width: 8px; height: 12px; border-radius: 2px; }
.al-bar-seg.filled-mood { background: var(--lavender); }
.al-bar-seg.filled-pleasure { background: var(--blush); }
.al-bar-seg.filled-mastery { background: var(--gold); }
.al-bar-seg.filled-avoidance { background: #b0c4de; }
.al-bar-seg.empty { background: rgba(255,255,255,0.06); }
.al-entry-notes { font-size: 0.875rem; color: var(--muted); margin-top: 0.75rem; font-style: italic; padding-top: 0.75rem; border-top: 1px solid var(--card-border); }
.al-delete-btn { background: none; border: none; color: var(--muted); cursor: pointer; padding: 0.25rem; border-radius: 6px; transition: color 0.2s; display: flex; align-items: center; }
.al-delete-btn:hover { color: var(--blush); }
.al-delete-btn svg { width: 15px; height: 15px; stroke: currentColor; fill: none; stroke-width: 2; }

/* ── AVOIDANCE AUDIT ── */
.aa-type-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 0.75rem; margin-top: 0.5rem; }
@media (max-width: 600px) { .aa-type-grid { grid-template-columns: 1fr; } }
.aa-type-btn {
  background: rgba(255,255,255,0.02); border: 1px solid var(--card-border);
  border-radius: 12px; padding: 1rem; cursor: pointer; transition: all 0.2s ease;
  display: flex; flex-direction: column; gap: 0.3rem;
}
.aa-type-btn:hover { border-color: var(--blush); background: rgba(232,200,212,0.05); }
.aa-type-btn.active { background: rgba(232,200,212,0.1); border-color: var(--blush); }
.aa-type-name { font-family: 'Cormorant Garamond', serif; font-size: 1.1rem; font-weight: 600; color: var(--blush); }
.aa-type-desc { font-size: 0.8rem; color: var(--muted); line-height: 1.4; }

.aa-entry-card {
  background: rgba(255,255,255,0.02); border: 1px solid var(--card-border);
  border-radius: 12px; padding: 1.25rem; margin-bottom: 0.75rem; transition: all 0.2s;
}
.aa-entry-card:hover { border-color: rgba(232,200,212,0.3); }
.aa-entry-header { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 1rem; padding-bottom: 0.75rem; border-bottom: 1px solid var(--card-border); }
.aa-entry-avoided { font-family: 'Cormorant Garamond', serif; font-size: 1.15rem; color: var(--text); font-style: italic; flex: 1; margin-right: 0.75rem; }
.aa-type-badge { padding: 0.25rem 0.7rem; border-radius: 20px; font-size: 0.75rem; font-weight: 500; background: rgba(232,200,212,0.15); color: var(--blush); flex-shrink: 0; }
.aa-entry-row { display: flex; gap: 0.5rem; margin-bottom: 0.5rem; }
.aa-entry-rowlabel { font-size: 0.8rem; color: var(--muted); min-width: 70px; font-style: italic; padding-top: 1px; }
.aa-entry-rowval { font-size: 0.875rem; color: var(--text); line-height: 1.5; }
.aa-entry-smallest { background: rgba(110,231,183,0.08); border: 1px solid rgba(110,231,183,0.2); border-radius: 8px; padding: 0.75rem; margin-top: 0.75rem; }
.aa-entry-smallest-label { font-size: 0.75rem; color: #6ee7b7; text-transform: uppercase; letter-spacing: 0.05em; margin-bottom: 0.25rem; }
.aa-entry-smallest-val { font-size: 0.9rem; color: var(--text); }
.aa-anxiety-bar { display: flex; gap: 3px; margin-top: 0.5rem; }
.aa-anxiety-seg { height: 8px; flex: 1; border-radius: 2px; }
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
    <button class="nav-tab" onclick="switchTab('activity-log')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><rect x="3" y="4" width="18" height="18" rx="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/><line x1="8" y1="14" x2="8" y2="14"/><line x1="12" y1="14" x2="12" y2="14"/><line x1="8" y1="17" x2="8" y2="17"/></svg>
      Activity Log
    </button>
    <button class="nav-tab" onclick="switchTab('avoidance-audit')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><path d="M10.29 3.86L1.82 18a2 2 0 0 0 1.71 3h16.94a2 2 0 0 0 1.71-3L13.71 3.86a2 2 0 0 0-3.42 0z"/><line x1="12" y1="9" x2="12" y2="13"/><line x1="12" y1="17" x2="12.01" y2="17"/></svg>
      Avoidance Audit
    </button>
    <button class="nav-tab" onclick="switchTab('wins-log')">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>
      Wins
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
            <button class="emotion-picker-toggle" onclick="toggleEmotionPicker()" type="button">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:14px;height:14px"><circle cx="12" cy="12" r="10"/><path d="M8 14s1.5 2 4 2 4-2 4-2"/><line x1="9" y1="9" x2="9.01" y2="9"/><line x1="15" y1="9" x2="15.01" y2="9"/></svg>
              Choose from list
            </button>
            <div class="emotion-picker-body" id="emotion-picker-body">
              <div class="emotion-category">
                <span class="emotion-category-label">😰 Anxiety &amp; Fear</span>
                <div class="emotion-chips">
                  <span class="emotion-chip" onclick="toggleEmotion(this)">anxious</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">afraid</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">panicked</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">worried</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">nervous</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">tense</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">overwhelmed</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">insecure</span>
                </div>
              </div>
              <div class="emotion-category">
                <span class="emotion-category-label">😢 Sadness &amp; Loss</span>
                <div class="emotion-chips">
                  <span class="emotion-chip" onclick="toggleEmotion(this)">sad</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">hopeless</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">lonely</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">empty</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">grieving</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">disappointed</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">heartbroken</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">helpless</span>
                </div>
              </div>
              <div class="emotion-category">
                <span class="emotion-category-label">😠 Anger &amp; Frustration</span>
                <div class="emotion-chips">
                  <span class="emotion-chip" onclick="toggleEmotion(this)">angry</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">frustrated</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">irritated</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">resentful</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">bitter</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">jealous</span>
                </div>
              </div>
              <div class="emotion-category">
                <span class="emotion-category-label">😳 Shame &amp; Guilt</span>
                <div class="emotion-chips">
                  <span class="emotion-chip" onclick="toggleEmotion(this)">ashamed</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">guilty</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">embarrassed</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">humiliated</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">inadequate</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">worthless</span>
                </div>
              </div>
              <div class="emotion-category">
                <span class="emotion-category-label">😮 Shock &amp; Confusion</span>
                <div class="emotion-chips">
                  <span class="emotion-chip" onclick="toggleEmotion(this)">confused</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">shocked</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">numb</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">disconnected</span>
                  <span class="emotion-chip" onclick="toggleEmotion(this)">lost</span>
                </div>
              </div>
            </div>
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
        <label class="section-label">What Would a Stranger Think?</label>
        <div class="helper-text">If a neutral observer — someone who doesn't know you — saw this situation, what would they objectively conclude? Not a friend, not an enemy. Just a fair stranger.</div>
        <textarea id="stranger-response" placeholder="A neutral observer would probably think..."></textarea>
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

      <div class="section">
        <label class="section-label">Emotion Intensity <span style="color:var(--muted);font-size:0.875rem;font-weight:300;">after reflection</span></label>
        <div class="helper-text">How intense does the emotion feel now, after completing this record?</div>
        <div style="display:flex;align-items:center;gap:1rem;">
          <input type="range" id="intensity-after" min="1" max="10" value="5" step="1" style="flex:1;">
          <div class="intensity-value" id="intensity-after-value">5</div>
        </div>
        <div id="intensity-shift-msg" style="font-size:0.85rem;color:var(--muted);font-style:italic;margin-top:0.5rem;min-height:1.2em;"></div>
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
      <div style="display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:0.75rem;margin-bottom:1.25rem;">
        <label class="section-label" style="margin:0;">Past Records</label>
        <div style="display:flex;align-items:center;gap:0.75rem;flex-wrap:wrap;">
          <button class="icon-btn" id="select-all-btn" onclick="toggleSelectAll()" style="font-size:0.82rem;padding:0.4rem 0.85rem;">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:14px;height:14px;"><rect x="3" y="3" width="18" height="18" rx="2"/><polyline points="9 12 11 14 15 10"/></svg>
            Select All
          </button>
          <div id="bulk-pdf-bar" style="display:none;align-items:center;gap:0.6rem;">
            <span id="selected-count" style="font-size:0.82rem;color:var(--lavender);font-weight:500;"></span>
            <button class="btn btn-primary" onclick="downloadSelectedPDF()" style="padding:0.45rem 1rem;font-size:0.85rem;">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:15px;height:15px;"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
              Download PDF
            </button>
            <button class="icon-btn" onclick="clearSelection()" style="font-size:0.82rem;padding:0.4rem 0.7rem;">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:14px;height:14px;"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
              Clear
            </button>
          </div>
        </div>
      </div>
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

  <!-- TAB: ACTIVITY LOG -->
  <div id="tab-activity-log" class="tab-content">
    <div class="card">
      <label class="section-label">Log an Activity</label>
      <div class="helper-text">Track what you do and how it makes you feel. Patterns will reveal themselves over time.</div>

      <div class="section" style="margin-top:1.5rem;">
        <label class="section-label" style="font-size:1.1rem;">What did you do?</label>
        <input type="text" id="al-activity" placeholder="e.g. went for a walk, replied to emails, called a friend...">
      </div>

      <div class="section">
        <label class="section-label" style="font-size:1.1rem;">When?</label>
        <input type="datetime-local" id="al-when" style="width:100%; background:rgba(255,255,255,0.02); border:1px solid var(--card-border); border-radius:12px; padding:0.85rem 1rem; color:var(--text); font-family:'Work Sans',sans-serif; font-size:1rem; transition:border-color 0.3s; cursor:pointer;" onfocus="this.style.borderColor='var(--lavender)'" onblur="this.style.borderColor='var(--card-border)'">
      </div>

      <div class="section">
        <label class="section-label" style="font-size:1.1rem;">Category</label>
        <div class="helper-text">What kind of activity was this?</div>
        <div class="al-category-grid">
          <div class="al-cat-btn active" data-cat="routine" onclick="selectCategory(this)">
            <span class="al-cat-icon">🔄</span>
            <span class="al-cat-name">Routine</span>
            <span class="al-cat-desc">Hygiene, meals, commute</span>
          </div>
          <div class="al-cat-btn" data-cat="necessary" onclick="selectCategory(this)">
            <span class="al-cat-icon">📋</span>
            <span class="al-cat-name">Necessary</span>
            <span class="al-cat-desc">Work, bills, appointments</span>
          </div>
          <div class="al-cat-btn" data-cat="pleasure" onclick="selectCategory(this)">
            <span class="al-cat-icon">✨</span>
            <span class="al-cat-name">Pleasure</span>
            <span class="al-cat-desc">Hobbies, rest, enjoyment</span>
          </div>
          <div class="al-cat-btn" data-cat="achievement" onclick="selectCategory(this)">
            <span class="al-cat-icon">🎯</span>
            <span class="al-cat-name">Achievement</span>
            <span class="al-cat-desc">Goals, growth, progress</span>
          </div>
        </div>
      </div>

      <div class="section">
        <label class="section-label" style="font-size:1.1rem;">Mood before</label>
        <div class="helper-text">How were you feeling before you did this?</div>
        <div class="al-rating-control">
          <input type="range" class="al-range" id="al-mood-before" min="1" max="10" value="5" oninput="document.getElementById('al-mood-before-val').textContent=this.value; updateMoodDelta()">
          <span class="al-rating-val" id="al-mood-before-val">5</span>
        </div>
      </div>

      <div class="section">
        <label class="section-label" style="font-size:1.1rem;">Mood after</label>
        <div class="helper-text">How did you feel once it was done?</div>
        <div class="al-rating-control">
          <input type="range" class="al-range" id="al-mood-after" min="1" max="10" value="5" oninput="document.getElementById('al-mood-after-val').textContent=this.value; updateMoodDelta()">
          <span class="al-rating-val" id="al-mood-after-val">5</span>
        </div>
        <div id="al-mood-delta" style="margin-top:0.75rem; font-size:0.9rem; color:var(--muted); font-style:italic; min-height:1.4em;"></div>
      </div>

      <div class="section">
        <label class="section-label" style="font-size:1.1rem;">Notes <span style="color:var(--muted);font-size:0.875rem;font-weight:300;">(optional)</span></label>
        <textarea id="al-notes" placeholder="Anything worth noting..." style="min-height:80px;"></textarea>
      </div>

      <div class="actions">
        <button class="btn btn-primary" onclick="saveActivityLog()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:18px;height:18px;"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"></path><polyline points="17 21 17 13 7 13 7 21"></polyline><polyline points="7 3 7 8 15 8"></polyline></svg>
          Save Entry
        </button>
        <button class="btn btn-secondary" onclick="clearActivityForm()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:18px;height:18px;"><polyline points="3 6 5 6 21 6"></polyline><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path></svg>
          Clear
        </button>
      </div>
    </div>

    <!-- Activity History -->
    <div class="card" id="al-history-card" style="display:none;">
      <label class="section-label">Activity History</label>
      <div class="helper-text" style="margin-bottom:1.5rem;">Your data over time. Look for patterns — not single data points.</div>
      <div class="stats-grid" style="margin-bottom:1.5rem;">
        <div class="stat-card"><div class="stat-value" id="al-total">0</div><div class="stat-label">Total Entries</div></div>
        <div class="stat-card"><div class="stat-value" id="al-avg-mood" style="color:var(--lavender);">-</div><div class="stat-label">Avg Mood Δ</div></div>
        <div class="stat-card"><div class="stat-value" id="al-top-cat" style="color:var(--gold);">-</div><div class="stat-label">Top Category</div></div>
      </div>
      <div class="chart-container" id="al-chart-container" style="height:220px; margin-bottom:1.5rem;"><canvas id="alMoodChart"></canvas></div>
      <div id="al-entries-container"></div>
    </div>
  </div>

  <!-- TAB: AVOIDANCE AUDIT -->
  <div id="tab-avoidance-audit" class="tab-content">
    <div class="card">
      <label class="section-label">Log an Avoidance</label>
      <div class="helper-text">No judgment here. Writing it down is the first act of approaching it.</div>

      <div class="section" style="margin-top:1.5rem;">
        <label class="section-label" style="font-size:1.1rem;">What did you avoid?</label>
        <div class="helper-text">Be specific — not "work" but "replying to that email from my manager"</div>
        <textarea id="aa-avoided" placeholder="What exactly did you avoid?" style="min-height:80px;"></textarea>
      </div>

      <div class="section">
        <label class="section-label" style="font-size:1.1rem;">What triggered the avoidance?</label>
        <div class="helper-text">What situation, thought, or feeling set it off?</div>
        <textarea id="aa-trigger" placeholder="What happened just before you avoided?" style="min-height:80px;"></textarea>
      </div>

      <div class="section">
        <label class="section-label" style="font-size:1.1rem;">How did you avoid it?</label>
        <div class="helper-text">What did you do instead?</div>
        <input type="text" id="aa-how" placeholder="e.g., scrolled phone, went to sleep, made tea...">
      </div>

      <div class="section">
        <label class="section-label" style="font-size:1.1rem;">Avoidance Type</label>
        <div class="helper-text">Knowing the type helps choose the right TRAC alternative</div>
        <div class="aa-type-grid">
          <div class="aa-type-btn active" data-type="behavioral" onclick="selectAvoidanceType(this)">
            <span class="aa-type-name">Behavioral</span>
            <span class="aa-type-desc">Left the situation, cancelled, didn't show up</span>
          </div>
          <div class="aa-type-btn" data-type="cognitive" onclick="selectAvoidanceType(this)">
            <span class="aa-type-name">Cognitive</span>
            <span class="aa-type-desc">Distracted yourself, suppressed thoughts, ruminated</span>
          </div>
          <div class="aa-type-btn" data-type="emotional" onclick="selectAvoidanceType(this)">
            <span class="aa-type-name">Emotional</span>
            <span class="aa-type-desc">Numbed out, used substances, dissociated</span>
          </div>
          <div class="aa-type-btn" data-type="social" onclick="selectAvoidanceType(this)">
            <span class="aa-type-name">Social</span>
            <span class="aa-type-desc">Withdrew from people, didn't reply, isolated</span>
          </div>
        </div>
      </div>

      <div class="section">
        <label class="section-label" style="font-size:1.1rem;">Anxiety before avoiding <span style="color:var(--muted); font-size:0.875rem;">(1–10)</span></label>
        <div class="al-rating-control" style="max-width:400px;">
          <input type="range" class="al-range" id="aa-anxiety" min="1" max="10" value="6" oninput="document.getElementById('aa-anxiety-val').textContent=this.value">
          <span class="al-rating-val" id="aa-anxiety-val">6</span>
        </div>
      </div>

      <div class="section">
        <label class="section-label" style="font-size:1.1rem;">What would the smallest version of this be?</label>
        <div class="helper-text">If you could only do 5% of this thing, what would that look like?</div>
        <input type="text" id="aa-smallest" placeholder="The smallest possible step toward it...">
      </div>

      <div class="section">
        <label class="section-label" style="font-size:1.1rem;">Notes <span style="color:var(--muted);font-size:0.875rem;font-weight:300;">(optional)</span></label>
        <textarea id="aa-notes" placeholder="Any other observations..." style="min-height:80px;"></textarea>
      </div>

      <div class="actions">
        <button class="btn btn-primary" onclick="saveAvoidanceLog()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:18px;height:18px;"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"></path><polyline points="17 21 17 13 7 13 7 21"></polyline><polyline points="7 3 7 8 15 8"></polyline></svg>
          Save Avoidance
        </button>
        <button class="btn btn-secondary" onclick="clearAvoidanceForm()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:18px;height:18px;"><polyline points="3 6 5 6 21 6"></polyline><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path></svg>
          Clear
        </button>
      </div>
    </div>

    <!-- Avoidance History -->
    <div class="card" id="aa-history-card" style="display:none;">
      <label class="section-label">Avoidance Audit</label>
      <div class="helper-text" style="margin-bottom:1.5rem;">Patterns you've named. Seeing them clearly is how you start changing them.</div>
      <div class="stats-grid" style="margin-bottom:1.5rem;">
        <div class="stat-card"><div class="stat-value" id="aa-total">0</div><div class="stat-label">Total Logged</div></div>
        <div class="stat-card"><div class="stat-value" id="aa-avg-anxiety" style="color:var(--blush);">-</div><div class="stat-label">Avg Anxiety</div></div>
        <div class="stat-card"><div class="stat-value" id="aa-top-type" style="color:var(--gold);">-</div><div class="stat-label">Top Type</div></div>
      </div>
      <div id="aa-entries-container"></div>
    </div>
  </div>

  <!-- TAB: WINS LOG -->
  <div id="tab-wins-log" class="tab-content">
    <div class="card">
      <label class="section-label">Log a Win</label>
      <div class="helper-text">Small or large. Handled something hard, noticed a distortion, spoke up, got out of bed on a bad day. All of it counts.</div>

      <div class="section" style="margin-top:1.5rem;">
        <label class="section-label" style="font-size:1.1rem;">What happened?</label>
        <textarea id="win-description" placeholder="Describe the win... be specific." style="min-height:90px;"></textarea>
      </div>

      <div class="section">
        <label class="section-label" style="font-size:1.1rem;">Category</label>
        <div class="aa-type-grid">
          <div class="win-cat-btn active" data-cat="coping" onclick="selectWinCategory(this)" style="background:rgba(255,255,255,0.02);border:1px solid var(--card-border);border-radius:12px;padding:1rem;cursor:pointer;transition:all 0.2s ease;display:flex;flex-direction:column;gap:0.3rem;">
            <span style="font-family:'Cormorant Garamond',serif;font-size:1.1rem;font-weight:600;color:var(--lavender);">Coping</span>
            <span style="font-size:0.8rem;color:var(--muted);line-height:1.4;">Managed anxiety, used a technique, stayed calm</span>
          </div>
          <div class="win-cat-btn" data-cat="social" onclick="selectWinCategory(this)" style="background:rgba(255,255,255,0.02);border:1px solid var(--card-border);border-radius:12px;padding:1rem;cursor:pointer;transition:all 0.2s ease;display:flex;flex-direction:column;gap:0.3rem;">
            <span style="font-family:'Cormorant Garamond',serif;font-size:1.1rem;font-weight:600;color:var(--blush);">Social</span>
            <span style="font-size:0.8rem;color:var(--muted);line-height:1.4;">Spoke up, reached out, set a boundary</span>
          </div>
          <div class="win-cat-btn" data-cat="task" onclick="selectWinCategory(this)" style="background:rgba(255,255,255,0.02);border:1px solid var(--card-border);border-radius:12px;padding:1rem;cursor:pointer;transition:all 0.2s ease;display:flex;flex-direction:column;gap:0.3rem;">
            <span style="font-family:'Cormorant Garamond',serif;font-size:1.1rem;font-weight:600;color:var(--gold);">Task</span>
            <span style="font-size:0.8rem;color:var(--muted);line-height:1.4;">Did something hard, showed up, followed through</span>
          </div>
          <div class="win-cat-btn" data-cat="self-awareness" onclick="selectWinCategory(this)" style="background:rgba(255,255,255,0.02);border:1px solid var(--card-border);border-radius:12px;padding:1rem;cursor:pointer;transition:all 0.2s ease;display:flex;flex-direction:column;gap:0.3rem;">
            <span style="font-family:'Cormorant Garamond',serif;font-size:1.1rem;font-weight:600;color:#6ee7b7;">Self-awareness</span>
            <span style="font-size:0.8rem;color:var(--muted);line-height:1.4;">Noticed a pattern, caught a distortion, reflected</span>
          </div>
        </div>
      </div>

      <div class="actions">
        <button class="btn btn-primary" onclick="saveWin()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:18px;height:18px;"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>
          Save Win
        </button>
        <button class="btn btn-secondary" onclick="clearWinForm()">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" style="width:18px;height:18px;"><polyline points="3 6 5 6 21 6"></polyline><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path></svg>
          Clear
        </button>
      </div>
    </div>

    <div class="card" id="wins-history-card" style="display:none;">
      <label class="section-label">Your Wins</label>
      <div class="helper-text" style="margin-bottom:1.5rem;">Evidence that you are more capable than you think. Read these on hard days.</div>
      <div class="stats-grid" style="margin-bottom:1.5rem;">
        <div class="stat-card"><div class="stat-value" id="wins-total">0</div><div class="stat-label">Total Wins</div></div>
        <div class="stat-card"><div class="stat-value" id="wins-this-week" style="color:var(--lavender);">0</div><div class="stat-label">This Week</div></div>
        <div class="stat-card"><div class="stat-value" id="wins-top-cat" style="color:var(--gold);">-</div><div class="stat-label">Top Category</div></div>
      </div>
      <div id="wins-entries-container"></div>
    </div>
  </div>



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
  if (msg.includes('User already registered') || msg.includes('already been registered')) return 'An account with this email already exists.';
  if (msg.includes('Invalid login credentials') || msg.includes('invalid_credentials')) return 'Incorrect email or password.';
  if (msg.includes('Email not confirmed')) return 'Please check your email and confirm your account first.';
  if (msg.includes('Too many requests') || msg.includes('rate limit')) return 'Too many attempts. Please try again later.';
  if (msg.includes('Password should be')) return 'Password must be at least 6 characters.';
  if (msg.includes('valid email') || msg.includes('invalid email')) return 'Please enter a valid email address.';
  if (msg.includes('Check your email')) return msg;
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
    if (data && (data.recordsJson || data.records_json || data.recordsJSON)) {
      cachedRecords = JSON.parse(data.recordsJson || data.records_json || data.recordsJSON);
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
      records_json: JSON.stringify(cachedRecords),
      updated_at: new Date().toISOString()
    });
    setSyncStatus('synced');
  } catch(e) {
    console.error('Save failed:', e.message);
    showMsg('✗ ' + e.message, true);
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
  else if (tabName === 'activity-log') {
    const whenEl = document.getElementById('al-when');
    if (whenEl && !whenEl.value) {
      const now = new Date();
      now.setMinutes(now.getMinutes() - now.getTimezoneOffset());
      whenEl.value = now.toISOString().slice(0, 16);
    }
    renderActivityHistory();
  }
  else if (tabName === 'avoidance-audit') renderAvoidanceHistory();
  else if (tabName === 'wins-log') renderWins();
}

// ══════════════════════════════════════════════════════════════════════════════
// INTENSITY SLIDER
// ══════════════════════════════════════════════════════════════════════════════
document.getElementById('intensity').addEventListener('input', (e) => {
  document.getElementById('intensity-value').textContent = e.target.value;
  updateIntensityShift();
});

document.getElementById('intensity-after').addEventListener('input', (e) => {
  document.getElementById('intensity-after-value').textContent = e.target.value;
  updateIntensityShift();
});

function updateIntensityShift() {
  const before = parseInt(document.getElementById('intensity').value);
  const after = parseInt(document.getElementById('intensity-after').value);
  const delta = after - before;
  const el = document.getElementById('intensity-shift-msg');
  if (!el) return;
  if (delta < 0) el.innerHTML = `<span style="color:#6ee7b7;">↓ ${delta} — the reflection helped.</span>`;
  else if (delta > 0) el.innerHTML = `<span style="color:#ff9bb3;">↑ +${delta} — still processing. That's okay.</span>`;
  else el.innerHTML = `<span style="color:var(--muted);">→ No change in intensity yet.</span>`;
}

// ══════════════════════════════════════════════════════════════════════════════
// COGNITIVE DISTORTIONS TOGGLE
// ══════════════════════════════════════════════════════════════════════════════
function toggleDistortion(el) { el.classList.toggle('selected'); }

// ══════════════════════════════════════════════════════════════════════════════
// EMOTION PICKER
// ══════════════════════════════════════════════════════════════════════════════
function toggleEmotionPicker() {
  const body = document.getElementById('emotion-picker-body');
  body.classList.toggle('open');
}

function toggleEmotion(chip) {
  chip.classList.toggle('selected');
  const selected = Array.from(document.querySelectorAll('#emotion-picker-body .emotion-chip.selected')).map(c => c.textContent);
  const input = document.getElementById('emotions');
  // Keep any manually typed content that is not in our chip list, then add selected chips
  const allChips = Array.from(document.querySelectorAll('#emotion-picker-body .emotion-chip')).map(c => c.textContent);
  const currentParts = input.value.split(',').map(s => s.trim()).filter(s => s && !allChips.includes(s));
  const merged = [...currentParts, ...selected];
  input.value = merged.join(', ');
}
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
    strangerResponse: document.getElementById('stranger-response').value,
    friendResponse: document.getElementById('friend-response').value,
    conclusion: document.getElementById('conclusion').value,
    intensityAfter: document.getElementById('intensity-after').value
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
    strangerResponse: document.getElementById('stranger-response').value,
    friendResponse: document.getElementById('friend-response').value,
    conclusion: document.getElementById('conclusion').value,
    intensityAfter: document.getElementById('intensity-after').value
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
  addSection('Emotions', record.emotions ? `${record.emotions} (${record.intensity}/10 before → ${record.intensityAfter || '?'}/10 after)` : '');
  addSection('Automatic Thoughts', record.thoughts);
  addSection('Evidence For', record.evidenceFor);
  addSection('Evidence Against', record.evidenceAgainst);
  addSection('Cognitive Distortions', record.distortions ? record.distortions.join(', ') : '');
  addSection('What Would a Stranger Think?', record.strangerResponse);
  addSection('If a Friend Said This...', record.friendResponse);
  addSection('Balanced Conclusion', record.conclusion);
  doc.save(`thought-record-${new Date(date).toISOString().split('T')[0]}.pdf`);
}

// ══════════════════════════════════════════════════════════════════════════════
// RENDER HISTORY
// ══════════════════════════════════════════════════════════════════════════════
let selectedRecordIndices = new Set();

function updateBulkBar() {
  const bar = document.getElementById('bulk-pdf-bar');
  const countEl = document.getElementById('selected-count');
  if (selectedRecordIndices.size > 0) {
    bar.style.display = 'flex';
    countEl.textContent = `${selectedRecordIndices.size} selected`;
  } else {
    bar.style.display = 'none';
  }
}

function toggleRecordSelect(realIndex) {
  if (selectedRecordIndices.has(realIndex)) {
    selectedRecordIndices.delete(realIndex);
  } else {
    selectedRecordIndices.add(realIndex);
  }
  const card = document.getElementById(`record-${realIndex}`);
  const cb = document.getElementById(`cb-${realIndex}`);
  if (card && cb) {
    cb.checked = selectedRecordIndices.has(realIndex);
    card.style.borderColor = selectedRecordIndices.has(realIndex) ? 'var(--lavender)' : 'var(--card-border)';
    card.style.background = selectedRecordIndices.has(realIndex) ? 'rgba(201,184,232,0.06)' : 'rgba(255,255,255,0.02)';
  }
  updateBulkBar();
}

function toggleSelectAll() {
  const sorted = [...cachedRecords].map((_, i) => i);
  if (selectedRecordIndices.size === cachedRecords.length) {
    clearSelection();
  } else {
    sorted.forEach(i => selectedRecordIndices.add(i));
    sorted.forEach(i => {
      const card = document.getElementById(`record-${i}`);
      const cb = document.getElementById(`cb-${i}`);
      if (card && cb) {
        cb.checked = true;
        card.style.borderColor = 'var(--lavender)';
        card.style.background = 'rgba(201,184,232,0.06)';
      }
    });
    updateBulkBar();
  }
}

function clearSelection() {
  selectedRecordIndices.forEach(i => {
    const card = document.getElementById(`record-${i}`);
    const cb = document.getElementById(`cb-${i}`);
    if (card && cb) {
      cb.checked = false;
      card.style.borderColor = 'var(--card-border)';
      card.style.background = 'rgba(255,255,255,0.02)';
    }
  });
  selectedRecordIndices.clear();
  updateBulkBar();
}

function downloadSelectedPDF() {
  const indices = Array.from(selectedRecordIndices).sort((a, b) => a - b);
  if (indices.length === 0) return;
  const records = indices.map(i => ({ record: cachedRecords[i], date: cachedRecords[i].timestamp }));
  generateBulkPDF(records);
}

function generateBulkPDF(items) {
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();
  const pageWidth = doc.internal.pageSize.getWidth();
  const pageHeight = doc.internal.pageSize.getHeight();
  const margin = 20;
  const maxWidth = pageWidth - 2 * margin;

  items.forEach((item, itemIdx) => {
    if (itemIdx > 0) doc.addPage();
    const record = item.record;
    let y = 20;

    // Header
    doc.setFontSize(18); doc.setTextColor(106, 90, 205);
    doc.text('Thought Record', margin, y); y += 9;
    doc.setFontSize(9); doc.setTextColor(150, 150, 150);
    doc.text(new Date(item.date).toLocaleString(), margin, y); y += 5;
    // Divider
    doc.setDrawColor(201, 184, 232); doc.setLineWidth(0.3);
    doc.line(margin, y, pageWidth - margin, y); y += 10;

    const addSection = (label, content) => {
      if (y > pageHeight - 25) { doc.addPage(); y = 20; }
      doc.setFontSize(10); doc.setTextColor(106, 90, 205); doc.setFont(undefined, 'bold');
      doc.text(label, margin, y); y += 6;
      doc.setFont(undefined, 'normal');
      if (content && content.trim()) {
        doc.setFontSize(9.5); doc.setTextColor(40, 40, 40);
        const lines = doc.splitTextToSize(content, maxWidth);
        lines.forEach(line => {
          if (y > pageHeight - 15) { doc.addPage(); y = 20; }
          doc.text(line, margin, y); y += 5;
        });
        y += 6;
      } else {
        doc.setFontSize(9); doc.setTextColor(160, 160, 160);
        doc.text('(not filled)', margin, y); y += 10;
      }
    };

    addSection('Situation', record.situation);
    if (record.emotions) {
      const emoLine = `${record.emotions}  ·  ${record.intensity}/10 before${record.intensityAfter ? ' → ' + record.intensityAfter + '/10 after' : ''}`;
      addSection('Emotions', emoLine);
    }
    addSection('Automatic Thoughts', record.thoughts);
    addSection('Evidence For', record.evidenceFor);
    addSection('Evidence Against', record.evidenceAgainst);
    if (record.distortions && record.distortions.length > 0) {
      addSection('Cognitive Distortions', record.distortions.join(', '));
    }
    if (record.strangerResponse) addSection('What Would a Stranger Think?', record.strangerResponse);
    addSection('If a Friend Said This...', record.friendResponse);
    addSection('Balanced Conclusion', record.conclusion);

    // Page number
    doc.setFontSize(8); doc.setTextColor(180, 180, 180);
    doc.text(`${itemIdx + 1} / ${items.length}`, pageWidth - margin, pageHeight - 8, { align: 'right' });
  });

  const dateStr = new Date().toISOString().split('T')[0];
  doc.save(`thought-records-${items.length}-entries-${dateStr}.pdf`);
  showMsg(`✓ Downloaded ${items.length} record${items.length > 1 ? 's' : ''}`, false);
}

function renderHistory() {
  const container = document.getElementById('records-container');
  if (cachedRecords.length === 0) { container.innerHTML = '<div class="no-records">No records yet. Save your first thought record!</div>'; return; }
  const sorted = [...cachedRecords].reverse();
  container.innerHTML = sorted.map((record, i) => {
    const realIndex = cachedRecords.length - 1 - i;
    const d = new Date(record.timestamp);
    const dateStr = d.toLocaleDateString('en-US', { weekday:'long', year:'numeric', month:'long', day:'numeric' }) + ' · ' + d.toLocaleTimeString('en-US', { hour:'2-digit', minute:'2-digit' });
    const isSelected = selectedRecordIndices.has(realIndex);
    return `
      <div class="record-card" id="record-${realIndex}" style="cursor:default;border-color:${isSelected ? 'var(--lavender)' : 'var(--card-border)'};background:${isSelected ? 'rgba(201,184,232,0.06)' : 'rgba(255,255,255,0.02)'};">
        <div class="record-header">
          <div style="display:flex;align-items:center;gap:0.75rem;flex:1;min-width:0;">
            <label style="display:flex;align-items:center;cursor:pointer;flex-shrink:0;" title="Select for bulk PDF" onclick="event.stopPropagation()">
              <input type="checkbox" id="cb-${realIndex}" ${isSelected ? 'checked' : ''} onchange="toggleRecordSelect(${realIndex})"
                style="width:16px;height:16px;accent-color:var(--lavender);cursor:pointer;flex-shrink:0;">
            </label>
            <div class="record-date" style="flex:1;min-width:0;">${dateStr}</div>
          </div>
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
          <textarea id="edit-stranger-response-${realIndex}" placeholder="What would a stranger think?">${record.strangerResponse || ''}</textarea>
          <textarea id="edit-friend-response-${realIndex}" placeholder="If a Friend Said This...">${record.friendResponse || ''}</textarea>
          <textarea id="edit-conclusion-${realIndex}" placeholder="Balanced Conclusion">${record.conclusion || ''}</textarea>
          <div style="margin-bottom:0.75rem;">
            <div style="font-size:0.85rem;color:var(--muted);margin-bottom:0.5rem;">Cognitive Distortions</div>
            <div class="distortion-tags" id="edit-distortions-${realIndex}">
              ${['All-or-Nothing','Overgeneralization','Catastrophizing','Mind Reading','Fortune Telling','Emotional Reasoning','Should Statements','Labeling','Personalization','Discounting the Positive'].map(d => `<span class="distortion-tag${record.distortions && record.distortions.includes(d) ? ' selected' : ''}" onclick="toggleDistortion(this)">${d}</span>`).join('')}
            </div>
          </div>
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
    strangerResponse: document.getElementById(`edit-stranger-response-${index}`).value,
    friendResponse: document.getElementById(`edit-friend-response-${index}`).value,
    conclusion: document.getElementById(`edit-conclusion-${index}`).value,
    distortions: Array.from(document.querySelectorAll(`#edit-distortions-${index} .distortion-tag.selected`)).map(el => el.textContent)
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
  ['situation','emotions','thoughts','evidence-for','evidence-against','stranger-response','friend-response','conclusion'].forEach(id => { const el = document.getElementById(id); if(el) el.value = ''; });
  document.getElementById('intensity').value = 5;
  document.getElementById('intensity-value').textContent = 5;
  document.getElementById('intensity-after').value = 5;
  document.getElementById('intensity-after-value').textContent = 5;
  const shiftMsg = document.getElementById('intensity-shift-msg');
  if (shiftMsg) shiftMsg.innerHTML = '';
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

// ══════════════════════════════════════════════════════════════════════════════
// ACTIVITY LOG
// ══════════════════════════════════════════════════════════════════════════════
let cachedActivityLogs = [];
let alMoodChart = null;

function updateMoodDelta() {
  const before = parseInt(document.getElementById('al-mood-before').value);
  const after = parseInt(document.getElementById('al-mood-after').value);
  const delta = after - before;
  const el = document.getElementById('al-mood-delta');
  if (delta > 0) el.innerHTML = `<span style="color:#6ee7b7;">↑ +${delta} mood improvement</span> — this activity helped.`;
  else if (delta < 0) el.innerHTML = `<span style="color:#ff9bb3;">↓ ${delta} mood drop</span> — worth noting.`;
  else el.innerHTML = `<span style="color:var(--muted);">→ No change</span> — neutral data is still useful.`;
}

function selectCategory(el) {
  document.querySelectorAll('.al-cat-btn').forEach(b => b.classList.remove('active'));
  el.classList.add('active');
}

function getSelectedCategory() {
  const btn = document.querySelector('.al-cat-btn.active');
  return btn ? btn.dataset.cat : 'routine';
}

function clearActivityForm() {
  document.getElementById('al-activity').value = '';
  document.getElementById('al-notes').value = '';
  document.getElementById('al-when').value = '';
  document.getElementById('al-mood-before').value = 5;
  document.getElementById('al-mood-before-val').textContent = 5;
  document.getElementById('al-mood-after').value = 5;
  document.getElementById('al-mood-after-val').textContent = 5;
  document.getElementById('al-mood-delta').innerHTML = '';
  document.querySelectorAll('.al-cat-btn').forEach((b,i) => b.classList.toggle('active', i===0));
}

async function saveActivityLog() {
  const activity = document.getElementById('al-activity').value.trim();
  if (!activity) { showMsg('✗ Please describe the activity', true); return; }
  const whenVal = document.getElementById('al-when').value;
  const entry = {
    id: Date.now(),
    timestamp: whenVal ? new Date(whenVal).toISOString() : new Date().toISOString(),
    activity,
    category: getSelectedCategory(),
    moodBefore: parseInt(document.getElementById('al-mood-before').value),
    moodAfter: parseInt(document.getElementById('al-mood-after').value),
    notes: document.getElementById('al-notes').value.trim()
  };
  cachedActivityLogs.unshift(entry);
  try {
    await saveAllData();
    showMsg('✓ Activity logged', false);
    clearActivityForm();
    renderActivityHistory();
  } catch(e) {
    cachedActivityLogs.shift();
    showMsg('✗ Save failed', true);
  }
}

async function deleteActivityLog(id) {
  if (!confirm('Delete this entry?')) return;
  const idx = cachedActivityLogs.findIndex(e => e.id === id);
  if (idx === -1) return;
  const removed = cachedActivityLogs.splice(idx, 1);
  try {
    await saveAllData();
    renderActivityHistory();
  } catch(e) {
    cachedActivityLogs.splice(idx, 0, removed[0]);
    showMsg('✗ Delete failed', true);
  }
}

function renderActivityHistory() {
  const card = document.getElementById('al-history-card');
  if (cachedActivityLogs.length === 0) { card.style.display = 'none'; return; }
  card.style.display = 'block';

  document.getElementById('al-total').textContent = cachedActivityLogs.length;

  // Avg mood delta
  const deltas = cachedActivityLogs.map(e => (e.moodAfter || 5) - (e.moodBefore || 5));
  const avgDelta = (deltas.reduce((s,d)=>s+d,0)/deltas.length);
  const avgDeltaEl = document.getElementById('al-avg-mood');
  avgDeltaEl.textContent = (avgDelta >= 0 ? '+' : '') + avgDelta.toFixed(1);
  avgDeltaEl.style.color = avgDelta > 0 ? '#6ee7b7' : avgDelta < 0 ? '#ff9bb3' : 'var(--lavender)';

  const catCounts = {};
  cachedActivityLogs.forEach(e => { catCounts[e.category] = (catCounts[e.category]||0)+1; });
  const topCat = Object.entries(catCounts).sort((a,b)=>b[1]-a[1])[0];
  const catLabels = { routine:'Routine', necessary:'Necessary', pleasure:'Pleasure', achievement:'Achieve' };
  document.getElementById('al-top-cat').textContent = topCat ? catLabels[topCat[0]] : '-';

  // Chart — before vs after mood
  const recent = [...cachedActivityLogs].reverse().slice(-14);
  const ctx = document.getElementById('alMoodChart');
  if (ctx) {
    if (alMoodChart) alMoodChart.destroy();
    alMoodChart = new Chart(ctx, {
      type: 'line',
      data: {
        labels: recent.map(e => {
          const d = new Date(e.timestamp);
          return d.toLocaleDateString('en', {month:'short', day:'numeric'});
        }),
        datasets: [
          { label: 'Before', data: recent.map(e => e.moodBefore || 5), borderColor: '#c9b8e8', backgroundColor: 'rgba(201,184,232,0.08)', tension: 0.4, fill: false },
          { label: 'After', data: recent.map(e => e.moodAfter || 5), borderColor: '#6ee7b7', backgroundColor: 'rgba(110,231,183,0.08)', tension: 0.4, fill: false }
        ]
      },
      options: {
        responsive: true, maintainAspectRatio: false,
        plugins: { legend: { labels: { color: '#e8e0f0', font: { size: 11 } } } },
        scales: {
          y: { min:1, max:10, ticks: { color:'#e8e0f0', stepSize:2 }, grid: { color:'rgba(255,255,255,0.06)' } },
          x: { ticks: { color:'#e8e0f0', font:{size:10} }, grid: { color:'rgba(255,255,255,0.06)' } }
        }
      }
    });
  }

  // Entries
  const container = document.getElementById('al-entries-container');
  container.innerHTML = cachedActivityLogs.map(entry => {
    const d = new Date(entry.timestamp);
    const dateStr = d.toLocaleDateString('en', {weekday:'short', month:'short', day:'numeric', hour:'2-digit', minute:'2-digit'});
    const before = entry.moodBefore || 5;
    const after = entry.moodAfter || 5;
    const delta = after - before;
    const deltaColor = delta > 0 ? '#6ee7b7' : delta < 0 ? '#ff9bb3' : 'var(--muted)';
    const deltaText = delta > 0 ? `↑ +${delta}` : delta < 0 ? `↓ ${delta}` : '→ 0';

    const moodBar = (val, color) => Array.from({length:10}, (_,i) =>
      `<div style="width:8px;height:12px;border-radius:2px;background:${i < val ? color : 'rgba(255,255,255,0.06)'};"></div>`
    ).join('');

    return `<div class="al-entry-card">
      <div class="al-entry-header">
        <div class="al-entry-activity">${entry.activity}</div>
        <div class="al-entry-meta">
          <span class="al-cat-pill ${entry.category}">${entry.category}</span>
          <button class="al-delete-btn" onclick="deleteActivityLog(${entry.id})"><svg viewBox="0 0 24 24"><polyline points="3 6 5 6 21 6"/><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6"/><line x1="10" y1="11" x2="10" y2="17"/><line x1="14" y1="11" x2="14" y2="17"/></svg></button>
        </div>
      </div>
      <div style="display:flex; gap:1.5rem; align-items:center; flex-wrap:wrap;">
        <div>
          <div style="font-size:0.72rem;color:var(--muted);margin-bottom:4px;text-transform:uppercase;letter-spacing:0.05em;">Before</div>
          <div style="display:flex;gap:2px;">${moodBar(before, '#c9b8e8')}</div>
          <div style="font-size:0.8rem;color:var(--lavender);margin-top:2px;">${before}/10</div>
        </div>
        <div style="font-size:1.5rem;color:${deltaColor};font-weight:600;">${deltaText}</div>
        <div>
          <div style="font-size:0.72rem;color:var(--muted);margin-bottom:4px;text-transform:uppercase;letter-spacing:0.05em;">After</div>
          <div style="display:flex;gap:2px;">${moodBar(after, '#6ee7b7')}</div>
          <div style="font-size:0.8rem;color:#6ee7b7;margin-top:2px;">${after}/10</div>
        </div>
      </div>
      <div class="al-entry-date" style="margin-top:0.6rem;">${dateStr}</div>
      ${entry.notes ? `<div class="al-entry-notes">${entry.notes}</div>` : ''}
    </div>`;
  }).join('');
}

// ══════════════════════════════════════════════════════════════════════════════
// WINS LOG
// ══════════════════════════════════════════════════════════════════════════════
let cachedWins = [];

function selectWinCategory(el) {
  document.querySelectorAll('.win-cat-btn').forEach(b => {
    b.style.background = 'rgba(255,255,255,0.02)';
    b.style.borderColor = 'var(--card-border)';
  });
  el.style.background = 'rgba(201,184,232,0.1)';
  el.style.borderColor = 'var(--lavender)';
}

function getSelectedWinCategory() {
  const btns = document.querySelectorAll('.win-cat-btn');
  for (const b of btns) {
    if (b.style.background.includes('0.1')) return b.dataset.cat;
  }
  return 'coping';
}

function clearWinForm() {
  const desc = document.getElementById('win-description');
  if (desc) desc.value = '';
  document.querySelectorAll('.win-cat-btn').forEach((b, i) => {
    b.style.background = 'rgba(255,255,255,0.02)';
    b.style.borderColor = 'var(--card-border)';
    if (i === 0) { b.style.background = 'rgba(201,184,232,0.1)'; b.style.borderColor = 'var(--lavender)'; }
  });
}

async function saveWin() {
  const desc = document.getElementById('win-description').value.trim();
  if (!desc) { showMsg('✗ Please describe the win', true); return; }
  const entry = {
    id: Date.now(),
    timestamp: new Date().toISOString(),
    description: desc,
    category: getSelectedWinCategory()
  };
  cachedWins.unshift(entry);
  try {
    await saveAllData();
    showMsg('✓ Win saved ★', false);
    clearWinForm();
    renderWins();
  } catch(e) {
    cachedWins.shift();
    showMsg('✗ Save failed', true);
  }
}

async function deleteWin(id) {
  if (!confirm('Delete this win?')) return;
  const idx = cachedWins.findIndex(e => e.id === id);
  if (idx === -1) return;
  const removed = cachedWins.splice(idx, 1);
  try {
    await saveAllData();
    renderWins();
  } catch(e) {
    cachedWins.splice(idx, 0, removed[0]);
    showMsg('✗ Delete failed', true);
  }
}

function renderWins() {
  const card = document.getElementById('wins-history-card');
  if (cachedWins.length === 0) { card.style.display = 'none'; return; }
  card.style.display = 'block';

  document.getElementById('wins-total').textContent = cachedWins.length;
  const weekAgo = new Date(); weekAgo.setDate(weekAgo.getDate() - 7);
  document.getElementById('wins-this-week').textContent = cachedWins.filter(w => new Date(w.timestamp) > weekAgo).length;
  const catCounts = {};
  cachedWins.forEach(w => { catCounts[w.category] = (catCounts[w.category]||0)+1; });
  const topCat = Object.entries(catCounts).sort((a,b)=>b[1]-a[1])[0];
  const catLabels = { coping:'Coping', social:'Social', task:'Task', 'self-awareness':'Awareness' };
  document.getElementById('wins-top-cat').textContent = topCat ? catLabels[topCat[0]] : '-';

  const catColors = { coping: 'var(--lavender)', social: 'var(--blush)', task: 'var(--gold)', 'self-awareness': '#6ee7b7' };

  const container = document.getElementById('wins-entries-container');
  container.innerHTML = cachedWins.map(entry => {
    const d = new Date(entry.timestamp);
    const dateStr = d.toLocaleDateString('en', {weekday:'short', month:'short', day:'numeric'}) + ' · ' + d.toLocaleTimeString('en', {hour:'2-digit', minute:'2-digit'});
    const color = catColors[entry.category] || 'var(--lavender)';
    return `<div style="background:rgba(255,255,255,0.02);border:1px solid var(--card-border);border-left:3px solid ${color};border-radius:12px;padding:1.25rem;margin-bottom:0.75rem;transition:all 0.2s;" onmouseover="this.style.borderColor='rgba(201,184,232,0.3)'" onmouseout="this.style.borderColor='var(--card-border)'">
      <div style="display:flex;justify-content:space-between;align-items:flex-start;gap:0.75rem;">
        <div style="font-family:'Cormorant Garamond',serif;font-size:1.1rem;color:var(--text);line-height:1.5;flex:1;">${entry.description}</div>
        <div style="display:flex;align-items:center;gap:0.5rem;flex-shrink:0;">
          <span style="padding:0.25rem 0.7rem;border-radius:20px;font-size:0.75rem;font-weight:500;background:rgba(255,255,255,0.06);color:${color};">${catLabels[entry.category]||entry.category}</span>
          <button class="al-delete-btn" onclick="deleteWin(${entry.id})"><svg viewBox="0 0 24 24"><polyline points="3 6 5 6 21 6"/><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6"/><line x1="10" y1="11" x2="10" y2="17"/><line x1="14" y1="11" x2="14" y2="17"/></svg></button>
        </div>
      </div>
      <div class="al-entry-date" style="margin-top:0.6rem;">${dateStr}</div>
    </div>`;
  }).join('');
}


let cachedAvoidanceLogs = [];

function selectAvoidanceType(el) {
  document.querySelectorAll('.aa-type-btn').forEach(b => b.classList.remove('active'));
  el.classList.add('active');
}

function getSelectedAvoidanceType() {
  const btn = document.querySelector('.aa-type-btn.active');
  return btn ? btn.dataset.type : 'behavioral';
}

function clearAvoidanceForm() {
  ['aa-avoided','aa-trigger','aa-how','aa-smallest','aa-notes'].forEach(id => {
    const el = document.getElementById(id); if(el) el.value = '';
  });
  const aaAnx = document.getElementById('aa-anxiety');
  if (aaAnx) { aaAnx.value = 6; aaAnx.dispatchEvent(new Event('input')); }
  document.querySelectorAll('.aa-type-btn').forEach((b,i) => b.classList.toggle('active', i===0));
}

async function saveAvoidanceLog() {
  const avoided = document.getElementById('aa-avoided').value.trim();
  if (!avoided) { showMsg('✗ Please describe what you avoided', true); return; }
  const entry = {
    id: Date.now(),
    timestamp: new Date().toISOString(),
    avoided,
    trigger: document.getElementById('aa-trigger').value.trim(),
    how: document.getElementById('aa-how').value.trim(),
    type: getSelectedAvoidanceType(),
    anxiety: parseInt(document.getElementById('aa-anxiety').value),
    smallest: document.getElementById('aa-smallest').value.trim(),
    notes: document.getElementById('aa-notes').value.trim()
  };
  cachedAvoidanceLogs.unshift(entry);
  try {
    await saveAllData();
    showMsg('✓ Avoidance logged', false);
    clearAvoidanceForm();
    renderAvoidanceHistory();
  } catch(e) {
    cachedAvoidanceLogs.shift();
    showMsg('✗ Save failed', true);
  }
}

async function deleteAvoidanceLog(id) {
  if (!confirm('Delete this entry?')) return;
  const idx = cachedAvoidanceLogs.findIndex(e => e.id === id);
  if (idx === -1) return;
  const removed = cachedAvoidanceLogs.splice(idx, 1);
  try {
    await saveAllData();
    renderAvoidanceHistory();
  } catch(e) {
    cachedAvoidanceLogs.splice(idx, 0, removed[0]);
    showMsg('✗ Delete failed', true);
  }
}

function renderAvoidanceHistory() {
  const card = document.getElementById('aa-history-card');
  if (cachedAvoidanceLogs.length === 0) { card.style.display = 'none'; return; }
  card.style.display = 'block';

  document.getElementById('aa-total').textContent = cachedAvoidanceLogs.length;
  const avgAnx = (cachedAvoidanceLogs.reduce((s,e)=>s+e.anxiety,0)/cachedAvoidanceLogs.length).toFixed(1);
  document.getElementById('aa-avg-anxiety').textContent = avgAnx;
  const typeCounts = {};
  cachedAvoidanceLogs.forEach(e => { typeCounts[e.type] = (typeCounts[e.type]||0)+1; });
  const topType = Object.entries(typeCounts).sort((a,b)=>b[1]-a[1])[0];
  const typeLabels = { behavioral:'Behavioral', cognitive:'Cognitive', emotional:'Emotional', social:'Social' };
  document.getElementById('aa-top-type').textContent = topType ? typeLabels[topType[0]] : '-';

  const container = document.getElementById('aa-entries-container');
  container.innerHTML = cachedAvoidanceLogs.map(entry => {
    const d = new Date(entry.timestamp);
    const dateStr = d.toLocaleDateString('en', {weekday:'short', month:'short', day:'numeric'}) + ' · ' + d.toLocaleTimeString('en', {hour:'2-digit', minute:'2-digit'});
    const anxBar = Array.from({length:10}, (_,i) => {
      const filled = i < entry.anxiety;
      const color = filled ? (entry.anxiety >= 8 ? '#ff9bb3' : entry.anxiety >= 5 ? '#d4a96a' : '#6ee7b7') : 'rgba(255,255,255,0.06)';
      return `<div class="aa-anxiety-seg" style="background:${color};"></div>`;
    }).join('');
    return `<div class="aa-entry-card">
      <div class="aa-entry-header">
        <div class="aa-entry-avoided">${entry.avoided}</div>
        <div style="display:flex;flex-direction:column;align-items:flex-end;gap:0.4rem;">
          <span class="aa-type-badge">${typeLabels[entry.type]||entry.type}</span>
          <button class="al-delete-btn" onclick="deleteAvoidanceLog(${entry.id})"><svg viewBox="0 0 24 24"><polyline points="3 6 5 6 21 6"/><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6"/><line x1="10" y1="11" x2="10" y2="17"/><line x1="14" y1="11" x2="14" y2="17"/></svg></button>
        </div>
      </div>
      ${entry.trigger ? `<div class="aa-entry-row"><span class="aa-entry-rowlabel">Trigger:</span><span class="aa-entry-rowval">${entry.trigger}</span></div>` : ''}
      ${entry.how ? `<div class="aa-entry-row"><span class="aa-entry-rowlabel">How:</span><span class="aa-entry-rowval">${entry.how}</span></div>` : ''}
      <div style="margin-top:0.5rem;">
        <div style="font-size:0.75rem;color:var(--muted);margin-bottom:0.3rem;">Anxiety: ${entry.anxiety}/10</div>
        <div class="aa-anxiety-bar">${anxBar}</div>
      </div>
      ${entry.smallest ? `<div class="aa-entry-smallest"><div class="aa-entry-smallest-label">Smallest version →</div><div class="aa-entry-smallest-val">${entry.smallest}</div></div>` : ''}
      <div class="al-entry-date" style="margin-top:0.75rem;">${dateStr}</div>
      ${entry.notes ? `<div class="al-entry-notes">${entry.notes}</div>` : ''}
    </div>`;
  }).join('');
}

// ══════════════════════════════════════════════════════════════════════════════
// UNIFIED CLOUD SAVE / LOAD (extends existing pattern)
// ══════════════════════════════════════════════════════════════════════════════
// Pack all three arrays into the single existing records_json column
// so no Supabase schema changes are needed
async function saveAllData() {
  setSyncStatus('syncing');
  try {
    const uid = FirebaseREST.currentUser.uid;
    const blob = JSON.stringify({
      v: 2,
      thoughtRecords: cachedRecords,
      activityLogs: cachedActivityLogs,
      avoidanceLogs: cachedAvoidanceLogs,
      wins: cachedWins
    });
    await FirebaseREST.setDocument('thoughtRecords', uid, {
      records_json: blob,
      updated_at: new Date().toISOString()
    });
    setSyncStatus('synced');
  } catch(e) {
    setSyncStatus('error');
    showMsg('✗ ' + e.message, true);
    throw e;
  }
}

// Override saveRecordsToCloud so thought records also go through saveAllData
saveRecordsToCloud = async function() {
  return saveAllData();
};

// Override loadRecordsFromCloud to unpack the blob or handle legacy format
loadRecordsFromCloud = async function() {
  try {
    setSyncStatus('syncing');
    const uid = FirebaseREST.currentUser.uid;
    const data = await FirebaseREST.getDocument('thoughtRecords', uid);
    if (data) {
      const raw = data.recordsJson || data.records_json || data.recordsJSON;
      if (raw) {
        const parsed = JSON.parse(raw);
        // v2 format: packed blob
        if (parsed && parsed.v === 2) {
          cachedRecords = parsed.thoughtRecords || [];
          cachedActivityLogs = parsed.activityLogs || [];
          cachedAvoidanceLogs = parsed.avoidanceLogs || [];
          cachedWins = parsed.wins || [];
        } else {
          // legacy: plain array of thought records
          cachedRecords = Array.isArray(parsed) ? parsed : [];
          cachedActivityLogs = [];
          cachedAvoidanceLogs = [];
          cachedWins = [];
        }
      } else {
        cachedRecords = []; cachedActivityLogs = []; cachedAvoidanceLogs = []; cachedWins = [];
      }
    } else {
      cachedRecords = []; cachedActivityLogs = []; cachedAvoidanceLogs = [];
    }
    setSyncStatus('synced');
    renderHistory();
    renderInsights();
    renderActivityHistory();
    renderAvoidanceHistory();
    renderWins();
  } catch(e) {
    console.error('Load failed:', e);
    setSyncStatus('error');
    cachedRecords = []; cachedActivityLogs = []; cachedAvoidanceLogs = [];
  }
};

handleSignOut = async function() {
  await FirebaseREST.signOut();
  cachedRecords = [];
  cachedActivityLogs = [];
  cachedAvoidanceLogs = [];
  cachedWins = [];
};
</script>

</body>
</html>
