# DESIGN.md — PREdistribuce365 Design systém
> Extrahováno z Figma screenshotů | Verze 0.1

---

## 1. Brand

- **Název portálu:** PREdistribuce365
- **Název společnosti:** PREdistribuce, a.s.
- **Logo:** Text "PRE" s červeným akcentem na "E" + text "PREdistribuce" vedle

---

## 2. Barevná paleta

```css
:root {
  /* Primární */
  --color-primary: #1a2f6e;        /* Tmavá námořní modrá — header, footer, CTA tlačítka, pravý panel */
  --color-primary-hover: #152560;  /* Hover stav primárních tlačítek */

  /* Akcent */
  --color-accent-red: #e30613;     /* Červená — logo akcent "E" */
  --color-accent-green: #5a7a2b;   /* Olivová zelená — tlačítko "Registrujte se", ikony v pravém panelu */
  --color-accent-green-hover: #4a6a20;

  /* Neutrální */
  --color-white: #ffffff;
  --color-background: #ffffff;     /* Bílé pozadí stránky */
  --color-border: #cccccc;         /* Tenký border inputů */
  --color-text-primary: #1a1a1a;   /* Hlavní text */
  --color-text-secondary: #555555; /* Sekundární text, popisky */
  --color-text-link: #1a2f6e;      /* Odkazy (Zapomenuté heslo) */

  /* Sémantické */
  --color-error-bg: #fdf0f0;       /* Pozadí chybové hlášky */
  --color-error-border: #e30613;   /* Levý border chybové hlášky */
  --color-error-icon: #e30613;     /* Ikona X v chybové hlásce */
  --color-error-title: #c0392b;    /* Nadpis chybové hlášky */

  /* Toggle aktivní tab */
  --color-toggle-active-bg: #1a2f6e;
  --color-toggle-active-text: #ffffff;
  --color-toggle-inactive-bg: #ffffff;
  --color-toggle-inactive-text: #1a2f6e;
  --color-toggle-border: #1a2f6e;
}
```

---

## 3. Typografie

```css
/* Font — systémový sans-serif, pravděpodobně Roboto nebo Inter */
font-family: 'Roboto', 'Inter', Arial, sans-serif;

/* Nadpisy stránek (H1) */
h1 {
  font-size: 32px;
  font-weight: 700;
  color: var(--color-text-primary);
  line-height: 1.2;
}

/* Popisky polí (label) */
label {
  font-size: 13px;
  font-weight: 400;
  color: var(--color-text-secondary);
  margin-bottom: 4px;
}

/* Body text */
body {
  font-size: 14px;
  font-weight: 400;
  color: var(--color-text-primary);
  line-height: 1.5;
}

/* Pravý panel — nadpis */
.panel-heading {
  font-size: 28px;
  font-weight: 700;
  color: #ffffff;
}
```

---

## 4. Layout stránek

Všechny auth stránky (přihlášení, registrace) sdílí stejný dvousloupcový layout:

```
┌─────────────────────────────────────────────────────┐
│  HEADER (celá šířka, tmavá modrá)                   │
├───────────────────────────┬─────────────────────────┤
│                           │                         │
│   LEVÝ SLOUPEC            │   PRAVÝ PANEL           │
│   (~55% šířky)            │   (~45% šířky)          │
│   Bílé pozadí             │   Tmavá modrá           │
│   Formulář                │   "Výhody portálu"      │
│                           │                         │
├───────────────────────────┴─────────────────────────┤
│  FOOTER (celá šířka, tmavá modrá)                   │
└─────────────────────────────────────────────────────┘
```

- Max-width obsahu: ~1100px, centrováno
- Levý sloupec padding: 60px vlevo, 40px vpravo
- Pravý panel: tmavá modrá pozadí, bílý text, padding 40px

---

## 5. Komponenty

### 5.1 Header
```css
.header {
  background: var(--color-primary);
  height: 56px;
  display: flex;
  align-items: center;
  padding: 0 40px;
}
/* Logo: bílý text "PREdistribuce" s červeným akcentem na "E" v logu */
```

### 5.2 Footer
```css
.footer {
  background: var(--color-primary);
  color: rgba(255,255,255,0.7);
  font-size: 12px;
  padding: 20px 40px;
  display: flex;
  justify-content: space-between;
}
/* Položky: Ochrana osobních údajů | Technická pomoc | Nastavení cookies | © 2025 PREdistribuce, a.s. */
```

### 5.3 Textový input
```css
input[type="text"],
input[type="email"],
input[type="password"] {
  width: 100%;
  height: 38px;
  border: 1px solid var(--color-border);
  border-radius: 0;              /* Žádné zaoblení rohů! */
  padding: 0 10px;
  font-size: 14px;
  background: #ffffff;
  box-sizing: border-box;
}
input:focus {
  outline: none;
  border-color: var(--color-primary);
}
/* Password field má ikonu oka vpravo (toggle zobrazení hesla) */
```

### 5.4 Primární tlačítko (modrá)
```css
.btn-primary {
  background: var(--color-primary);
  color: #ffffff;
  border: none;
  border-radius: 0;              /* Žádné zaoblení rohů! */
  padding: 10px 28px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  min-width: 140px;
}
.btn-primary:hover {
  background: var(--color-primary-hover);
}
/* Příklady: "Přihlásit se", "Založit" */
```

### 5.5 Sekundární tlačítko (zelená)
```css
.btn-secondary {
  background: var(--color-accent-green);
  color: #ffffff;
  border: none;
  border-radius: 0;
  padding: 10px 28px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
}
.btn-secondary:hover {
  background: var(--color-accent-green-hover);
}
/* Příklad: "Registrujte se" */
```

### 5.6 Textový odkaz
```css
.link {
  color: var(--color-primary);
  font-size: 14px;
  text-decoration: none;
  cursor: pointer;
}
.link:hover {
  text-decoration: underline;
}
/* Příklady: "Zapomenuté heslo", "Přihlaste se" */
```

### 5.7 Toggle Domácnost / Firma
```css
.toggle-group {
  display: flex;
  border: 1px solid var(--color-toggle-border);
  width: fit-content;
  margin-bottom: 20px;
}
.toggle-option {
  padding: 8px 24px;
  font-size: 14px;
  cursor: pointer;
  background: var(--color-toggle-inactive-bg);
  color: var(--color-toggle-inactive-text);
}
.toggle-option.active {
  background: var(--color-toggle-active-bg);
  color: var(--color-toggle-active-text);
}
/* Aktivní tab má checkmark fajfku vpravo od textu */
```

### 5.8 Chybová hláška
```css
.error-box {
  border: 1px solid #e8c0c0;
  border-left: 4px solid var(--color-error-border);
  background: var(--color-error-bg);
  padding: 14px 16px;
  margin: 16px 0;
  display: flex;
  gap: 12px;
  align-items: flex-start;
}
.error-icon {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: var(--color-error-icon);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 12px;
  flex-shrink: 0;
}
.error-title {
  font-size: 14px;
  font-weight: 600;
  color: var(--color-error-title);
  margin-bottom: 4px;
}
.error-text {
  font-size: 13px;
  color: var(--color-text-primary);
  line-height: 1.5;
}
```

### 5.9 Pravý panel "Výhody"
```css
.benefits-panel {
  background: var(--color-primary);
  color: #ffffff;
  padding: 40px;
}
.benefits-panel h2 {
  font-size: 28px;
  font-weight: 700;
  margin-bottom: 28px;
}
.benefit-item {
  display: flex;
  align-items: flex-start;
  gap: 14px;
  margin-bottom: 20px;
}
.benefit-icon {
  width: 36px;
  height: 36px;
  border-radius: 6px;
  background: var(--color-accent-green);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.benefit-text {
  font-size: 14px;
  color: rgba(255,255,255,0.9);
  line-height: 1.5;
}
```

### 5.10 "Ještě nemáte účet?" box
```css
.register-box {
  border: 1px solid var(--color-border);
  padding: 20px 24px;
  margin-top: 24px;
}
.register-box p {
  font-size: 15px;
  font-weight: 500;
  margin-bottom: 12px;
}
```

### 5.11 Tooltip (nápověda k poli)
```css
/* Malá ikona ⓘ vedle labelu pole */
/* Po hoveru zobrazí bílý box s textem a tmavým pozadím */
.tooltip-trigger {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  border: 1px solid var(--color-border);
  font-size: 11px;
  color: var(--color-text-secondary);
  cursor: help;
  margin-left: 6px;
}
.tooltip-content {
  background: #333333;
  color: #ffffff;
  font-size: 12px;
  padding: 10px 14px;
  border-radius: 4px;
  max-width: 280px;
  line-height: 1.5;
}
```

---

## 6. Specifická pravidla stránek

### Přihlášení
- H1: "Přihlášení do PREdistribuce365"
- Pole: E-mail, Heslo (s toggle zobrazení)
- Chybový stav: červený box s ikonou X, nadpis "Chyba přihlášení", popis chyby + kontakt na zákaznickou linku
- Pod formulářem: tlačítko "Přihlásit se" + link "Zapomenuté heslo" (inline, stejná řada)
- Dole: box "Ještě nemáte účet?" + zelené tlačítko "Registrujte se"

### Registrace (Založení účtu)
- H1: "Založení PREdistribuce365"
- Toggle: Domácnost / Firma (Firma = aktivní tab má checkmark + modrá výplň)
- Pole Domácnost: EAN (s tooltip ⓘ), E-mail
- Pole Firma navíc: IČO
- Tlačítko: "Založit" (modrá, primární)
- Link: "Už máte účet? Přihlaste se"

---

## 7. Design principy (odvozené ze screenshotů)

- **Žádné border-radius** na tlačítkách a inputech — ostrý korporátní styl
- **Minimalistické inputy** — tenký border, bílé pozadí, žádné stíny
- **Dvousloupcový layout** vždy — formulář vlevo, marketing vpravo
- **Pravý panel vždy tmavě modrý** s bílým textem a zelenými ikonami
- **Chybové hlášky jsou výrazné** — levý červený border, světle červené pozadí
- **Dva typy tlačítek:** primární (modrá = akce v portálu) a sekundární (zelená = registrace/onboarding)

---

*Soubor bude doplňován s dalšími screenshoty.*
