# Misja na Talerzu — Landing Page Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a responsive, single-page landing page for "Misja na Talerzu" culinary workshops based on the approved JPG design.

**Architecture:** Pure HTML + CSS, no frameworks. One `index.html` file with a linked `style.css`. Google Fonts for typography. Smooth scroll navigation. Mobile-first responsive with hamburger menu.

**Tech Stack:** HTML5, CSS3, Google Fonts (Poppins + Lato)

---

### Task 1: Project scaffold — CSS file, Google Fonts, CSS reset & variables

**Files:**
- Create: `style.css`
- Modify: `index.html`

**Step 1: Create `style.css` with reset, variables, and base typography**

```css
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700;800&family=Lato:wght@400;700&display=swap');

:root {
  --orange: #E8791D;
  --orange-light: #F5943E;
  --green-dark: #1B5E20;
  --green: #2E7D32;
  --green-light: #388E3C;
  --white: #FFFFFF;
  --dark: #1A1A1A;
  --gray-light: #F5F5F5;
  --font-heading: 'Poppins', sans-serif;
  --font-body: 'Lato', sans-serif;
}

*, *::before, *::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
  font-size: 16px;
}

body {
  font-family: var(--font-body);
  color: var(--dark);
  line-height: 1.6;
  overflow-x: hidden;
}

h1, h2, h3, h4 {
  font-family: var(--font-heading);
  line-height: 1.2;
}

a {
  text-decoration: none;
  color: inherit;
}

ul {
  list-style: none;
}

img {
  max-width: 100%;
  height: auto;
  display: block;
}

.container {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 20px;
}
```

**Step 2: Update `index.html` to link the stylesheet and set up base structure**

Replace entire `index.html` with:

```html
<!DOCTYPE html>
<html lang="pl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Misja na Talerzu — Warsztaty kulinarne</title>
  <meta name="description" content="Indywidualne warsztaty gotowania w Oswiecimiu. Naucz sie gotowac zdrowo, smacznie i bez stresu.">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <!-- Sections will be added in subsequent tasks -->
</body>
</html>
```

**Step 3: Verify in browser**

Open `http://localhost:8080`. Expect blank white page, no console errors, Poppins/Lato fonts loading in Network tab.

**Step 4: Commit**

```bash
git add style.css index.html
git commit -m "feat: project scaffold with CSS reset, variables, Google Fonts"
```

---

### Task 2: Sticky navbar with mobile hamburger

**Files:**
- Modify: `index.html` (add `<nav>` inside `<body>`)
- Modify: `style.css` (add navbar styles)

**Step 1: Add navbar HTML to `index.html`**

Insert at top of `<body>`:

```html
<nav class="navbar" id="navbar">
  <div class="container navbar__inner">
    <a href="#home" class="navbar__logo">
      <span class="navbar__logo-top">MISJA</span>
      <span class="navbar__logo-bottom">NA TALERZU</span>
    </a>
    <button class="navbar__toggle" id="navToggle" aria-label="Menu">
      <span></span><span></span><span></span>
    </button>
    <ul class="navbar__links" id="navLinks">
      <li><a href="#home">HOME</a></li>
      <li><a href="#warsztaty">O WARSZTATACH</a></li>
      <li><a href="#gdzie">GDZIE I JAK?</a></li>
      <li><a href="#omnie">O MNIE</a></li>
      <li><a href="#kontakt">KONTAKT</a></li>
    </ul>
  </div>
</nav>
```

**Step 2: Add navbar CSS to `style.css`**

```css
/* === NAVBAR === */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background: var(--white);
  z-index: 1000;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}

.navbar__inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 20px;
}

.navbar__logo {
  display: flex;
  flex-direction: column;
  font-family: var(--font-heading);
  font-weight: 800;
  line-height: 1;
  color: var(--green-dark);
}

.navbar__logo-top {
  font-size: 1.1rem;
}

.navbar__logo-bottom {
  font-size: 0.7rem;
  letter-spacing: 0.1em;
}

.navbar__links {
  display: flex;
  gap: 24px;
}

.navbar__links a {
  font-family: var(--font-heading);
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--dark);
  transition: color 0.2s;
}

.navbar__links a:hover {
  color: var(--orange);
}

.navbar__toggle {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 5px;
}

.navbar__toggle span {
  display: block;
  width: 25px;
  height: 3px;
  background: var(--dark);
  border-radius: 2px;
  transition: 0.3s;
}

@media (max-width: 768px) {
  .navbar__toggle {
    display: flex;
  }
  .navbar__links {
    display: none;
    flex-direction: column;
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    background: var(--white);
    padding: 20px;
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    gap: 16px;
  }
  .navbar__links.active {
    display: flex;
  }
}
```

**Step 3: Add hamburger toggle JS at bottom of `<body>` in `index.html`**

```html
<script>
  document.getElementById('navToggle').addEventListener('click', function() {
    document.getElementById('navLinks').classList.toggle('active');
  });
  document.querySelectorAll('.navbar__links a').forEach(function(link) {
    link.addEventListener('click', function() {
      document.getElementById('navLinks').classList.remove('active');
    });
  });
</script>
```

**Step 4: Verify in browser**

- Desktop: white sticky bar with logo left, 5 links right
- Mobile (< 768px): hamburger icon, clicking opens vertical menu
- Clicking a link closes the menu

**Step 5: Commit**

```bash
git add index.html style.css
git commit -m "feat: sticky navbar with mobile hamburger menu"
```

---

### Task 3: Hero section

**Files:**
- Modify: `index.html` (add hero section after `</nav>`)
- Modify: `style.css` (add hero styles)

**Step 1: Add hero HTML**

Insert after `</nav>`:

```html
<section class="hero" id="home">
  <div class="hero__bg">
    <div class="container hero__content">
      <div class="hero__logo-large">
        <span class="hero__logo-misja">MISJA</span>
        <span class="hero__logo-na">NA TALERZU</span>
      </div>
      <div class="hero__main">
        <div class="hero__photo-placeholder">
          <div class="hero__photo-circle"></div>
        </div>
        <div class="hero__text">
          <h1>MISJA NA TALERZU</h1>
          <p class="hero__tagline">Indywidualne warsztaty kulinarne, które pokazują, że zdrowe gotowanie może być proste, sycące, naprawdę smaczne i na każdą kieszeń.</p>
          <p class="hero__desc">Warsztaty to propozycja dla osób, które szukają czegoś więcej niż kolejnej diety. To okazja, by odblokować kuchnię w praktycznym, przyjaznym stylu — bez poradników, za&nbsp;to z&nbsp;prawdziwą praktyką. Pokażę Ci jak gotować mądrze, tanio i&nbsp;zdrowo — tak, żeby posiłki były szybkie, pyszne i&nbsp;dopasowane do Twojego trybu życia. Bez zbędnego stresu, bez wyrzutów — za&nbsp;to z&nbsp;uśmiechem, rozmową i&nbsp;wiedzą, która naprawdę przydaje się w&nbsp;życiu.</p>
          <a href="#kontakt" class="btn btn--orange">Umów swoją kulinarną misję</a>
        </div>
      </div>
    </div>
  </div>
</section>
```

**Step 2: Add hero CSS**

```css
/* === HERO === */
.hero {
  padding-top: 60px; /* offset for fixed navbar */
}

.hero__bg {
  background: var(--green);
  position: relative;
  overflow: hidden;
  padding: 60px 0 80px;
}

.hero__logo-large {
  text-align: center;
  color: var(--white);
  font-family: var(--font-heading);
  font-weight: 800;
  margin-bottom: 40px;
}

.hero__logo-misja {
  display: block;
  font-size: 3rem;
}

.hero__logo-na {
  display: block;
  font-size: 1.5rem;
  letter-spacing: 0.15em;
}

.hero__main {
  display: flex;
  align-items: center;
  gap: 40px;
}

.hero__photo-placeholder {
  flex-shrink: 0;
}

.hero__photo-circle {
  width: 280px;
  height: 280px;
  border-radius: 50%;
  background: var(--green-dark);
  border: 4px solid var(--orange);
}

.hero__text {
  color: var(--white);
}

.hero__text h1 {
  font-size: 2rem;
  margin-bottom: 12px;
}

.hero__tagline {
  font-size: 1.1rem;
  font-weight: 700;
  margin-bottom: 16px;
}

.hero__desc {
  font-size: 0.95rem;
  margin-bottom: 24px;
  opacity: 0.95;
}

/* === BUTTONS === */
.btn {
  display: inline-block;
  padding: 14px 32px;
  border-radius: 30px;
  font-family: var(--font-heading);
  font-weight: 700;
  font-size: 1rem;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
  text-align: center;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0,0,0,0.2);
}

.btn--orange {
  background: var(--orange);
  color: var(--white);
}

.btn--green {
  background: var(--green-dark);
  color: var(--white);
}

@media (max-width: 768px) {
  .hero__main {
    flex-direction: column;
    text-align: center;
  }
  .hero__photo-circle {
    width: 200px;
    height: 200px;
  }
  .hero__logo-misja {
    font-size: 2.2rem;
  }
  .hero__logo-na {
    font-size: 1.1rem;
  }
}
```

**Step 3: Verify in browser**

- Green section with large centered "MISJA NA TALERZU" logo text
- Below: dark circle placeholder (left) + white text (right)
- Orange CTA button at bottom
- On mobile: stacks vertically, centered

**Step 4: Commit**

```bash
git add index.html style.css
git commit -m "feat: hero section with logo, tagline, CTA"
```

---

### Task 4: "Dla kogo" section (orange background)

**Files:**
- Modify: `index.html` (add section after hero)
- Modify: `style.css` (add section styles)

**Step 1: Add HTML**

Insert after `</section>` (hero):

```html
<section class="dla-kogo" id="warsztaty">
  <div class="container">
    <h2>DLA KOGO JEST „MISJA NA TALERZU"<br>I CO Z NIEJ WYNIESIESZ?</h2>
    <div class="dla-kogo__intro">
      <p>„Misja na talerzu" jest dla Ciebie, jeśli chcesz jeść zdrowiej, ale nie masz pojęcia, od czego zacząć, jeśli myślisz, że nie umiesz gotować — a wystarczy tylko ktoś, kto Cię poprowadzi. Pokażę Ci, jak gotować prosto, zdrowo i ekonomicznie, podpowiem Ci sztuczki, które sprawią, że zyskasz pewność i radość z bycia w kuchni na co dzień.</p>
    </div>
    <div class="dla-kogo__columns">
      <div class="dla-kogo__col">
        <h3>Dla kogo są warsztaty?</h3>
        <ul>
          <li>chcesz jeść zdrowiej, ale nie wiesz, jak zacząć</li>
          <li>myślisz, że nie umiesz gotować</li>
          <li>jesteś zmęczona dietami i efektem jojo</li>
          <li>nie masz czasu na planowanie posiłków</li>
          <li>chcesz przemycać więcej warzyw i owoców</li>
          <li>nie wiesz, jak komponować zbilansowane posiłki</li>
          <li>chcesz czerpać przyjemność z gotowania</li>
          <li>chcesz kupować sprytnie, bez przepłacania</li>
        </ul>
      </div>
      <div class="dla-kogo__col">
        <h3>Co zyskujesz?</h3>
        <ul>
          <li>uczysz się robić szybkie, zdrowe posiłki, które naprawdę smakują</li>
          <li>dostajesz menu dopasowane do siebie — gotowe dania zabierasz do domu</li>
          <li>poznajesz tipy i triki kulinarne do natychmiastowego wdrożenia</li>
          <li>uczysz się planowania zakupów i gotowania bez marnowania</li>
          <li>przełamujesz blokadę przed gotowaniem</li>
          <li>otrzymujesz domowe dodatki: autorska wegeta, lista produktów i akcesoriów „must&nbsp;have"</li>
        </ul>
      </div>
    </div>
    <p class="dla-kogo__motto"><em>To nie kurs dietetyczny. To kulinarna misja — dla tych, którzy chcą żyć lepiej, jeść mądrzej i gotować z przyjemnością.</em></p>
  </div>
</section>
```

**Step 2: Add CSS**

```css
/* === DLA KOGO === */
.dla-kogo {
  background: var(--orange);
  color: var(--white);
  padding: 60px 0;
}

.dla-kogo h2 {
  text-align: center;
  font-size: 1.8rem;
  margin-bottom: 24px;
}

.dla-kogo__intro {
  max-width: 800px;
  margin: 0 auto 32px;
  text-align: center;
  font-size: 1rem;
}

.dla-kogo__columns {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  margin-bottom: 32px;
}

.dla-kogo__col h3 {
  font-size: 1.2rem;
  margin-bottom: 16px;
}

.dla-kogo__col ul {
  list-style: none;
}

.dla-kogo__col li {
  padding-left: 24px;
  position: relative;
  margin-bottom: 10px;
  font-size: 0.95rem;
}

.dla-kogo__col li::before {
  content: '✓';
  position: absolute;
  left: 0;
  font-weight: 700;
}

.dla-kogo__motto {
  text-align: center;
  font-size: 1.05rem;
  max-width: 700px;
  margin: 0 auto;
}

@media (max-width: 768px) {
  .dla-kogo__columns {
    grid-template-columns: 1fr;
    gap: 24px;
  }
  .dla-kogo h2 {
    font-size: 1.4rem;
  }
}
```

**Step 3: Verify** — orange section with centered heading, two columns of checkmarked lists, italic motto.

**Step 4: Commit**

```bash
git add index.html style.css
git commit -m "feat: 'dla kogo' section with target audience and benefits"
```

---

### Task 5: "Gdzie i jak?" + "Jak wygląda warsztat?" section

**Files:**
- Modify: `index.html`
- Modify: `style.css`

**Step 1: Add HTML**

```html
<section class="gdzie" id="gdzie">
  <div class="container">
    <div class="gdzie__columns">
      <div class="gdzie__col">
        <h2>GDZIE I JAK?</h2>
        <h3>Informacje organizacyjne</h3>
        <ul>
          <li>Oświęcim i okolice</li>
          <li>oferta dla mieszkańców Małopolski i&nbsp;Śląska</li>
          <li>spotkania indywidualne 1:1 (w&nbsp;przyszłości także małe grupy)</li>
          <li>czas trwania: ok. 3 godziny</li>
          <li>możliwość organizacji zakupów za moje pośrednictwem</li>
        </ul>
      </div>
      <div class="gdzie__col">
        <h2>JAK WYGLĄDA WARSZTAT?</h2>
        <h3>Jak wygląda nasza kulinarna misja?</h3>
        <ul>
          <li>wspólnie ustalamy co chcesz ugotować, ile to ma kosztować i&nbsp;na ile osób — tworzę menu</li>
          <li>warsztat trwa ok. 3 godziny (z&nbsp;możliwością rozszerzenia)</li>
          <li>nie ma jednego schematu — to nie fabryka gotowania, a w&nbsp;100% Twoje potrzeby</li>
          <li>dostosowuję się do Twojego poziomu, tempa i&nbsp;możliwości</li>
          <li>gotowe posiłki zabierasz do domu — jeszcze ciepłe, pachnące i&nbsp;pyszne</li>
          <li>na spotkaniu korzystamy gotujemy w&nbsp;dobrze wyposażonej kuchni z&nbsp;dużym blatem i&nbsp;wyspą</li>
          <li>na koniec rozmawiamy o zakupach — podpowiem co i gdzie kupić taniej</li>
        </ul>
        <p class="gdzie__note">Bez oceniania. Bez presji. Za to z ogromem praktycznej wiedzy, którą możesz od razu stosować na co dzień.</p>
      </div>
    </div>
    <div class="gdzie__cta">
      <a href="#kontakt" class="btn btn--orange">CHCĘ WZIĄĆ UDZIAŁ</a>
    </div>
  </div>
</section>
```

**Step 2: Add CSS**

```css
/* === GDZIE I JAK === */
.gdzie {
  background: var(--white);
  padding: 60px 0;
}

.gdzie__columns {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
}

.gdzie h2 {
  font-size: 1.6rem;
  color: var(--green-dark);
  margin-bottom: 8px;
}

.gdzie h3 {
  font-size: 1rem;
  color: var(--orange);
  margin-bottom: 16px;
}

.gdzie ul {
  list-style: none;
}

.gdzie li {
  padding-left: 20px;
  position: relative;
  margin-bottom: 10px;
  font-size: 0.95rem;
}

.gdzie li::before {
  content: '•';
  position: absolute;
  left: 0;
  color: var(--orange);
  font-weight: 700;
}

.gdzie__note {
  margin-top: 16px;
  font-style: italic;
  font-size: 0.95rem;
  color: #555;
}

.gdzie__cta {
  text-align: center;
  margin-top: 40px;
}

@media (max-width: 768px) {
  .gdzie__columns {
    grid-template-columns: 1fr;
  }
}
```

**Step 3: Verify** — white section, two columns, green headings, orange subheadings, bulleted lists, centered CTA.

**Step 4: Commit**

```bash
git add index.html style.css
git commit -m "feat: 'gdzie i jak' and 'jak wyglada warsztat' sections"
```

---

### Task 6: "O mnie" section

**Files:**
- Modify: `index.html`
- Modify: `style.css`

**Step 1: Add HTML**

```html
<section class="omnie" id="omnie">
  <div class="container omnie__inner">
    <div class="omnie__photo">
      <div class="omnie__photo-circle"></div>
    </div>
    <div class="omnie__text">
      <h2>O MNIE</h2>
      <h3>Kim jestem i dlaczego powstała „Misja na Talerzu"?</h3>
      <p class="omnie__name">Agata Olejniczak</p>
      <p>Jestem energiczną, charyzmatyczną kucharką z doświadczeniem w marketingu i pasją do zdrowego stylu życia. Wierzę, że gotowanie powinno być radością, a nie obowiązkiem.</p>
      <p>„Misja na talerzu" powstała z obserwacji, jak wiele osób chce jeść zdrowiej, ale czuje się zagubionych — w natłoku informacji, gotowych diet, produktów w sklepach. Pokazuję, że gotowanie domowe może być szybkie, proste, pyszne i ekonomiczne. Dzielę się wiedzą, doświadczeniem i uśmiechem — a reszta idzie sama.</p>
    </div>
  </div>
</section>
```

**Step 2: Add CSS**

```css
/* === O MNIE === */
.omnie {
  background: var(--white);
  padding: 60px 0;
}

.omnie__inner {
  display: flex;
  align-items: center;
  gap: 40px;
  max-width: 800px;
  margin: 0 auto;
}

.omnie__photo-circle {
  width: 200px;
  height: 200px;
  border-radius: 50%;
  background: var(--green);
  flex-shrink: 0;
  border: 4px solid var(--orange);
}

.omnie h2 {
  font-size: 1.6rem;
  color: var(--green-dark);
  margin-bottom: 4px;
}

.omnie h3 {
  font-size: 1rem;
  color: var(--orange);
  margin-bottom: 12px;
}

.omnie__name {
  font-family: var(--font-heading);
  font-weight: 700;
  font-size: 1.2rem;
  margin-bottom: 12px;
}

.omnie p {
  font-size: 0.95rem;
  margin-bottom: 10px;
}

@media (max-width: 768px) {
  .omnie__inner {
    flex-direction: column;
    text-align: center;
  }
  .omnie__photo-circle {
    width: 160px;
    height: 160px;
  }
}
```

**Step 3: Verify** — centered layout, round green placeholder (left), text with name (right).

**Step 4: Commit**

```bash
git add index.html style.css
git commit -m "feat: 'o mnie' section with bio placeholder"
```

---

### Task 7: "Decluttering kuchni" section

**Files:**
- Modify: `index.html`
- Modify: `style.css`

**Step 1: Add HTML**

```html
<section class="declutter">
  <div class="container declutter__inner">
    <div class="declutter__photo">
      <div class="declutter__photo-rect"></div>
    </div>
    <div class="declutter__text">
      <h2>DECLUTTERING KUCHNI</h2>
      <p class="declutter__subtitle">Decluttering kuchni — bo dobra kuchnia to taka, która ułatwia życie.</p>
      <p>Na życzenie moich kursantów mogę również zadbać o Twoją kuchnię — ocenić wyposażenie, poradzić co zostawić, co wymienić.</p>
      <h3>Pomogę Ci:</h3>
      <ul>
        <li>ocenić sprzęty i narzędzia — wyrzucić to, co przeszkadza, zostawić to, co potrzebne</li>
        <li>uporządkować kuchnię tak, by gotowanie było łatwiejsze i&nbsp;przyjemniejsze</li>
        <li>przejrzeć produkty spożywcze — daty, jakość, przydatność</li>
        <li>stworzyć system, który sprawi, że kuchnia będzie miejscem, w&nbsp;którym lubisz przebywać</li>
      </ul>
      <p>Bo każda kuchnia może być zapraszająca, zdrowa i Twoja — wystarczy po prostu być świadomą.</p>
    </div>
  </div>
</section>
```

**Step 2: Add CSS**

```css
/* === DECLUTTERING === */
.declutter {
  background: var(--green);
  color: var(--white);
  padding: 60px 0;
}

.declutter__inner {
  display: flex;
  align-items: center;
  gap: 40px;
}

.declutter__photo-rect {
  width: 280px;
  height: 200px;
  border-radius: 16px;
  background: var(--green-dark);
  flex-shrink: 0;
}

.declutter h2 {
  font-size: 1.6rem;
  margin-bottom: 8px;
}

.declutter__subtitle {
  font-weight: 700;
  margin-bottom: 12px;
}

.declutter h3 {
  margin-bottom: 12px;
  font-size: 1rem;
}

.declutter li {
  padding-left: 20px;
  position: relative;
  margin-bottom: 8px;
  font-size: 0.95rem;
}

.declutter li::before {
  content: '•';
  position: absolute;
  left: 0;
}

.declutter p {
  font-size: 0.95rem;
  margin-bottom: 10px;
}

@media (max-width: 768px) {
  .declutter__inner {
    flex-direction: column;
  }
  .declutter__photo-rect {
    width: 100%;
    height: 180px;
  }
}
```

**Step 3: Verify** — green section, image placeholder left, text with bullet list right.

**Step 4: Commit**

```bash
git add index.html style.css
git commit -m "feat: 'decluttering kuchni' section"
```

---

### Task 8: Contact section + footer

**Files:**
- Modify: `index.html`
- Modify: `style.css`

**Step 1: Add contact HTML**

```html
<section class="kontakt" id="kontakt">
  <div class="container">
    <h2>KONTAKT</h2>
    <p class="kontakt__subtitle">Chcesz wziąć udział w „Misji na talerzu"?</p>
    <p class="kontakt__desc">Napisz do mnie i umów swoją kulinarną misję.</p>
    <div class="kontakt__columns">
      <div class="kontakt__info">
        <p><span class="kontakt__icon">✉</span> misjanalerzu@gmail.com</p>
        <p><span class="kontakt__icon">📞</span> +48 843 693 86</p>
        <p><span class="kontakt__icon">📷</span> @misjaNaTalerzu</p>
      </div>
      <form class="kontakt__form" onsubmit="return false;">
        <input type="text" placeholder="Imię:" aria-label="Imię">
        <input type="tel" placeholder="Telefon:" aria-label="Telefon">
        <textarea placeholder="Wiadomość:" rows="4" aria-label="Wiadomość"></textarea>
        <button type="submit" class="btn btn--orange">Wyślij zgłoszenie</button>
      </form>
    </div>
  </div>
</section>
```

**Step 2: Add footer HTML**

```html
<footer class="footer">
  <div class="container footer__inner">
    <div class="footer__logo">
      <span class="footer__logo-top">MISJA</span>
      <span class="footer__logo-bottom">NA TALERZU</span>
    </div>
    <ul class="footer__links">
      <li><a href="#home">HOME</a></li>
      <li><a href="#warsztaty">O WARSZTATACH</a></li>
      <li><a href="#gdzie">GDZIE I JAK?</a></li>
      <li><a href="#omnie">O MNIE</a></li>
      <li><a href="#kontakt">KONTAKT</a></li>
    </ul>
  </div>
</footer>
```

**Step 3: Add CSS**

```css
/* === KONTAKT === */
.kontakt {
  background: var(--white);
  padding: 60px 0;
}

.kontakt h2 {
  font-size: 1.8rem;
  color: var(--green-dark);
  margin-bottom: 8px;
}

.kontakt__subtitle {
  font-family: var(--font-heading);
  font-weight: 700;
  font-size: 1.1rem;
  margin-bottom: 4px;
}

.kontakt__desc {
  color: #555;
  margin-bottom: 32px;
}

.kontakt__columns {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  align-items: start;
}

.kontakt__info p {
  margin-bottom: 12px;
  font-size: 1rem;
}

.kontakt__icon {
  margin-right: 8px;
}

.kontakt__form input,
.kontakt__form textarea {
  width: 100%;
  padding: 12px 16px;
  border: 2px solid #ddd;
  border-radius: 8px;
  font-family: var(--font-body);
  font-size: 0.95rem;
  margin-bottom: 12px;
  transition: border-color 0.2s;
}

.kontakt__form input:focus,
.kontakt__form textarea:focus {
  outline: none;
  border-color: var(--orange);
}

.kontakt__form .btn {
  width: 100%;
}

/* === FOOTER === */
.footer {
  background: var(--green-dark);
  color: var(--white);
  padding: 30px 0;
}

.footer__inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.footer__logo {
  font-family: var(--font-heading);
  font-weight: 800;
  line-height: 1;
}

.footer__logo-top {
  display: block;
  font-size: 1.1rem;
}

.footer__logo-bottom {
  display: block;
  font-size: 0.7rem;
  letter-spacing: 0.1em;
}

.footer__links {
  display: flex;
  gap: 20px;
}

.footer__links a {
  font-family: var(--font-heading);
  font-size: 0.8rem;
  font-weight: 600;
  color: var(--white);
  transition: color 0.2s;
}

.footer__links a:hover {
  color: var(--orange);
}

@media (max-width: 768px) {
  .kontakt__columns {
    grid-template-columns: 1fr;
  }
  .footer__inner {
    flex-direction: column;
    gap: 16px;
    text-align: center;
  }
  .footer__links {
    flex-wrap: wrap;
    justify-content: center;
  }
}
```

**Step 4: Verify** — contact section with info left, form right. Footer with logo and links.

**Step 5: Commit**

```bash
git add index.html style.css
git commit -m "feat: contact section and footer"
```

---

### Task 9: Final polish — visual refinements

**Files:**
- Modify: `style.css`

**Step 1: Add separator between "O mnie" and "Gdzie i jak" sections**

Add a subtle top border to the `omnie` section to visually separate it from `gdzie`:

```css
.omnie {
  border-top: 3px solid var(--orange);
}
```

**Step 2: Ensure consistent section spacing and smooth scroll offset**

Verify all `id` anchors scroll correctly with the fixed navbar. Adjust scroll offset if needed:

```css
section[id] {
  scroll-margin-top: 70px;
}
```

**Step 3: Verify full page top-to-bottom**

- All nav links scroll to correct sections
- All sections match design layout and colors
- Mobile responsive (hamburger, single columns)
- No horizontal overflow on any viewport

**Step 4: Commit**

```bash
git add style.css
git commit -m "feat: final visual polish and scroll offset fixes"
```
