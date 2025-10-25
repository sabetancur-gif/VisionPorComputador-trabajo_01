---
title: "Taller 1: Fundamentos y calibración de cámara"
description: "Visión por Computador — Universidad Nacional de Colombia — Taller 1: calibración, transformaciones y segmentación."
layout: default
permalink: /
theme: minimal   
---

```css
/* Fuentes */
@import url('[https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&display=swap](https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&display=swap)');

:root{
  --bg:#f6f8fb;
  --card:#ffffff;
  --muted:#6b7280;
  --accent:#0f172a;
  --accent-2:#0ea5a4;
  --maxw:1200px;
}

/* Reset / body */
html,body{height:100%}
body{
  margin:0;
  padding:28px;
  font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
  background:linear-gradient(180deg,#fbfdff 0%, var(--bg) 100%);
  color:var(--accent);
  -webkit-font-smoothing:antialiased;
}

/* Layout */
.pro-wrapper{
  max-width: var(--maxw);
  margin: 0 auto;
  display: grid;
  grid-template-columns: 320px 1fr;
  gap: 28px;
  align-items: start;
  box-sizing: border-box;
  padding-bottom: 64px;
}

/* Sidebar */
#toc-sidebar{
  position: sticky;
  top: 28px;
  background: var(--card);
  border-radius: 12px;
  padding: 18px;
  box-shadow: 0 8px 24px rgba(11,15,30,0.06);
  border: 1px solid rgba(15,23,42,0.04);
  height: calc(100vh - 56px);
  overflow: auto;
}
#toc-sidebar h4{margin:0 0 10px 0;color:var(--accent-2);font-size:13px}
#toc-list{list-style:none;padding:0;margin:0}
#toc-list li{margin:8px 0;font-size:14px}
#toc-list li.h3{margin-left:10px;font-size:13px;color:var(--muted)}
#toc-list a{color:var(--accent);text-decoration:none}
#toc-list a:hover{text-decoration:underline}

/* Main content */
.pro-content{background:transparent;word-break:break-word}
.header-card{
  background:var(--card);
  padding:18px;
  border-radius:12px;
  box-shadow:0 8px 24px rgba(11,15,30,0.06);
  border:1px solid rgba(15,23,42,0.04);
  margin-bottom:18px;
}
.header-meta{display:flex;gap:20px;flex-wrap:wrap;color:var(--muted);font-size:14px}
.pro-content h1{font-size:28px;margin-top:4px;margin-bottom:8px}
.pro-content h2{font-size:20px;margin-top:28px;margin-bottom:8px}
.pro-content h3{font-size:16px;margin-top:18px;margin-bottom:6px}
.pro-content p{margin:8px 0;color:#10203a}
.pro-content ul{margin:6px 0 12px 20px}
.pro-content pre{background:#0b1220;color:#e6eef6;padding:12px;border-radius:8px;overflow:auto}

/* Section cards */
.section-card{
  background: var(--card);
  padding:20px;
  border-radius:12px;
  margin-bottom:18px;
  border: 1px solid rgba(15,23,42,0.04);
  box-shadow: 0 6px 18px rgba(11,15,30,0.03);
}

/* Floating actions */
.top-actions{
  position: fixed;
  right: 18px;
  bottom: 18px;
  display:flex;
  flex-direction:column;
  gap:10px;
  z-index:1200;
}
.btn{
  display:inline-flex;align-items:center;gap:8px;padding:10px 14px;background:var(--accent-2);color:white;border-radius:12px;border:none;box-shadow:0 8px 18px rgba(14,165,164,0.18);cursor:pointer;font-weight:700;text-decoration:none;font-size:14px;
}
.btn.secondary{background:#0f172a;padding:9px 12px}

.muted{color:var(--muted);font-size:13px}

/* Responsive */
@media (max-width:980px){
  .pro-wrapper{grid-template-columns:1fr;padding:0 12px}
  #toc-sidebar{position:relative;top:0;height:auto;margin-bottom:14px}
}

@media print{
  body{background:white;padding:0}
  #toc-sidebar{display:none}
  .pro-wrapper{grid-template-columns:1fr}
}

/* Smooth anchor scroll */
html { scroll-behavior: smooth; }

