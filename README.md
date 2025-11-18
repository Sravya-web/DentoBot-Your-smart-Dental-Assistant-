/* Mobile-first responsive styles */
:root{
  --bg:#ffffff;
  --muted:#6b7280;
  --accent:#0b74de;
  --card:#f8fafc;
  --radius:12px;
  --max:1100px;
  font-family: Inter, system-ui, Arial, sans-serif;
}

*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:#0f172a;line-height:1.5}
.container{max-width:var(--max);margin:0 auto;padding:1rem}
.header-inner{display:flex;align-items:center;justify-content:space-between}
.brand{font-weight:700;text-decoration:none;color:var(--accent);font-size:1.1rem}
.nav{display:none;gap:1rem}
.nav a{color:var(--muted);text-decoration:none;font-size:0.95rem}
.nav-toggle{background:none;border:1px solid #e6e9ef;padding:0.35rem 0.6rem;border-radius:8px}
.site-header{background:#fff;position:sticky;top:0;z-index:40;border-bottom:1px solid #eee}
.hero{display:block;padding:1.25rem 0;gap:1rem}
.hero-text h1{margin:0 0 0.5rem;font-size:1.4rem}
.hero-img img{max-width:100%;display:block;border-radius:12px;background:#f3f4f6}
.btn{display:inline-block;padding:0.6rem 1rem;border-radius:10px;text-decoration:none;background:var(--accent);color:#fff}
.btn.ghost{background:transparent;border:1px solid #d1d5db;color:var(--muted)}
.card{background:var(--card);padding:1rem;border-radius:12px;margin:1rem 0}
.persona-grid{display:grid;grid-template-columns:1fr 1fr;gap:0.75rem}
.wireframes-grid, .screens-grid{display:grid;grid-template-columns:1fr;gap:0.75rem}
.screens-grid img, .wireframes-grid img{width:100%;border-radius:8px;display:block}

/* modal */
.modal{position:fixed;inset:0;background:rgba(0,0,0,0.6);display:none;align-items:center;justify-content:center;padding:1rem}
.modal img{max-width:92%;max-height:80vh;border-radius:8px}
.modal-close{position:absolute;right:1rem;top:1rem;background:#fff;border-radius:999px;border:0;padding:0.4rem 0.6rem}

/* large screens */
@media(min-width:800px){
  .hero{display:grid;grid-template-columns:1fr 420px;align-items:center}
  .nav{display:flex}
  .persona-grid{grid-template-columns:repeat(2,1fr)}
  .wireframes-grid, .screens-grid{grid-template-columns:repeat(3,1fr)}
  .hero-text h1{font-size:2rem}
}


// small interactions: nav toggle + image modal
document.addEventListener('DOMContentLoaded', () => {
  const navToggle = document.getElementById('navToggle');
  const mainNav = document.getElementById('mainNav');
  navToggle.addEventListener('click', () => {
    mainNav.classList.toggle('open');
    if (mainNav.classList.contains('open')) {
      mainNav.style.display = 'flex';
    } else {
      mainNav.style.display = '';
    }
  });

  // Image modal
  const modal = document.getElementById('imgModal');
  const modalImg = document.getElementById('modalImg');
  const modalClose = document.getElementById('modalClose');

  document.querySelectorAll('.screens-grid img, .wireframes-grid img').forEach(img => {
    img.style.cursor = 'zoom-in';
    img.addEventListener('click', (e) => {
      modalImg.src = img.dataset.large || img.src;
      modal.style.display = 'flex';
      modal.setAttribute('aria-hidden', 'false');
    });
  });

  modalClose.addEventListener('click', () => {
    modal.style.display = 'none';
    modal.setAttribute('aria-hidden', 'true');
    modalImg.src = '';
  });

  // Close on overlay click
  modal.addEventListener('click', (e) => {
    if (e.target === modal) {
      modalClose.click();
    }
  });
});




