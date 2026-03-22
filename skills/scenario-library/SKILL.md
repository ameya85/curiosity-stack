---
name: scenario-library
description: >
  Activate when user says "I don't know what to research", "give me ideas",
  "what can I decompose", "show me scenarios", "browse topics", "not sure where
  to start", "what topics are available", or runs /curiosity-stack:scenarios.
  Also activate on first session if local.md session_count is 0 or empty —
  surface the library automatically after the welcome message.
  Never activate mid-decomposition.
---

# Scenario Library

## Purpose

A curated library of 18 pre-built decomposition starting points organised into
6 categories. Removes the blank-slate problem for new users. Each scenario
launches the decomposition directly when selected — no copying, no pasting.

---

## Display

Generate an interactive HTML artifact using the design system below.

**Design system:**
- Background: `#fafaf8`
- Text: `#2c2c2c` primary, `#6b6558` secondary
- Accent: `#1b5e52` (teal)
- Borders: `0.5px solid #e0ddd6`
- Border radius: 12px cards, 8px chips
- Font: system-ui
- Attribution badge top: `⬡ Curiosity Stack · Scenario Library · v3.2.2`

**Layout:**
- Search bar at top
- Category tabs: All / India Themes / Geopolitics / Global Trends / AI / Cybersecurity / Energy & Climate
- When AI tab is active — show sub-filter: All AI / Global AI / AI — India
- Card grid: `repeat(auto-fill, minmax(210px, 1fr))`
- Preview panel below grid when card is selected

**Each card shows:**
- Category dot + label (color-coded)
- Topic title (13px, font-weight 500)
- 2-line description (12px, muted)
- Estimated session time
- "Preview →" button

**Preview panel shows:**
- Category label
- Topic title
- Full description + "The plugin walks you through all 6 layers — one question at a time."
- 7 layer chips — each showing layer label + what it reveals for this specific topic
- "Start decomposition →" button (PRIMARY ACTION)
- "Dismiss" button (secondary, text only)
- Estimated time

---

## Critical — Start decomposition button behaviour

The "Start decomposition →" button MUST use this exact JavaScript pattern:

```javascript
function startDecomposition(title) {
  const prompt = 'Help me understand the value chain for: ' + title;
  
  // Primary: try sendPrompt() — fires directly into chat
  if (typeof sendPrompt === 'function') {
    sendPrompt(prompt);
    return;
  }
  
  // Fallback: copy to clipboard with clear visual feedback
  if (navigator.clipboard && navigator.clipboard.writeText) {
    navigator.clipboard.writeText(prompt).then(() => {
      showCopiedFeedback();
    }).catch(() => {
      showManualCopy(prompt);
    });
  } else {
    showManualCopy(prompt);
  }
}

function showCopiedFeedback() {
  const btn = document.getElementById('startBtn');
  const original = btn.innerHTML;
  btn.innerHTML = '✓ Prompt copied — paste into chat';
  btn.style.background = '#166534';
  btn.disabled = true;
  setTimeout(() => {
    btn.innerHTML = original;
    btn.style.background = '';
    btn.disabled = false;
  }, 3000);
}

function showManualCopy(prompt) {
  // Show the prompt text in a selectable box
  document.getElementById('manualCopyBox').style.display = 'block';
  document.getElementById('manualCopyText').value = prompt;
  document.getElementById('manualCopyText').select();
}
```

**The UI must include:**
- A primary green "Start decomposition →" button with id="startBtn"
- A hidden fallback box with id="manualCopyBox" that shows only if clipboard fails:
  ```html
  <div id="manualCopyBox" style="display:none; margin-top:12px;">
    <p style="font-size:12px; color:#6b6558; margin-bottom:6px;">
      Copy this and paste into the chat:
    </p>
    <textarea id="manualCopyText" readonly 
      style="width:100%; padding:8px; font-size:13px; 
             border:1px solid #e0ddd6; border-radius:6px;
             background:#f8f8f6; resize:none; height:56px;">
    </textarea>
  </div>
  ```

**Never show "Copy prompt" as the primary button label.**
The primary button always says "Start decomposition →".
Only show copy-related UI as a fallback when sendPrompt() is unavailable.

---

## Categories and Scenarios

### 🇮🇳 India Themes
Color: `#1b5e52`

1. **Semiconductor packaging in India** (8 min)
   Where does India sit in the global OSAT value chain and what are the build requirements?
   L0: TSMC dependency signal | L1: What OSAT actually does | L2: Geopolitical root causes | L3: India fab solution space | L4: Capital, talent, land needs | L5: India players + global comps | L6: Listed vs pre-IPO access

2. **India defence manufacturing** (9 min)
   Post-PLI, what is India actually building and who sits in the supply chain?
   L0: Indigenisation push | L1: What gets made locally | L2: Import dependency causes | L3: Solution categories by segment | L4: Tech + capital requirements | L5: HAL, BEL, private OEMs | L6: Listed vs defence funds

3. **India GCC opportunity** (8 min)
   Global Capability Centres expanding in India — where is value actually accumulating?
   L0: MNC investment surge | L1: What GCCs actually do | L2: Why India wins this | L3: Service + infra industries | L4: Talent, RE, connectivity | L5: Service cos, RE players | L6: How to access this theme

4. **Pharma API supply chain** (8 min)
   India is the pharmacy of the world. What does the value chain actually look like?
   L0: API dependency headlines | L1: What APIs are and who needs them | L2: China concentration root cause | L3: API + CDMO solution space | L4: Chemistry, regulatory, capex | L5: Divi's, Laurus, Aurobindo | L6: Listed plays + CDMO funds

---

### 🌍 Geopolitics
Color: `#993c1d`

5. **Middle East conflict → oil supply** (9 min)
6. **Russia-Ukraine → energy transition** (9 min)
7. **US-China tariffs → supply chain** (10 min)
8. **Taiwan risk → semiconductor chain** (9 min)

---

### 🌐 Global Trends
Color: `#185fa5`

9. **Space economy infrastructure** (9 min)
10. **Precision medicine data layer** (9 min)

---

### 🤖 AI — Global
Color: `#533ab7`

11. **AI inference demand** (8 min)
12. **AI data centre infrastructure** (9 min)

---

### 🤖 AI — India
Color: `#7c3aed`

13. **Indian IT services in the AI era** (10 min)
14. **India AI data annotation layer** (8 min)

---

### 🔒 Cybersecurity
Color: `#3b6d11`

15. **Enterprise cybersecurity demand** (9 min)
16. **OT security in critical infrastructure** (9 min)

---

### ⚡ Energy & Climate
Color: `#854f0b`

17. **Grid-scale battery storage** (9 min)
18. **Green hydrogen economy** (9 min)

---

## After scenario launches

The curiosity-framework skill picks up the topic and begins at Layer 0.
Apply all normal post-output flows from output-generator skill after completion.
