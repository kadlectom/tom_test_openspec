# PRD — Zákaznický portál distributora elektrické energie
> Verze: 0.2 (mock) | Datum: 2026-03 | Scope: Domácnosti — MVP

---

## 1. Kontext a cíl projektu

Distributor elektrické energie potřebuje zákaznický samoobslužný portál, prostřednictvím kterého budou zákazníci (domácnosti, v budoucnu i firmy) spravovat svá odběrná místa, podávat žádosti o služby a komunikovat s distributorem bez nutnosti telefonického nebo osobního kontaktu.

**Cíl MVP:** Umožnit zákazníkovi z kategorie Domácnost registraci, přihlášení, výběr profilu, přehled odběrných míst a podání žádostí o distribuční služby prostřednictvím sekce „Potřebuji zařídit".

---

## 2. Uživatelské role

| Role | Popis |
|---|---|
| **Majitel OM** | Zákazník, který je smluvním vlastníkem odběrného místa. Plná správa. |
| **Dodatečný uživatel** | Osoba pověřená správou OM majitelem. Omezená práva dle nastavení majitele. |

> Firma jako typ zákazníka je v roadmapě, ale není součástí MVP.

---

## 3. Architektura stránek (scope)

### 3.1 Veřejná zóna (před přihlášením)

- **Přihlášení** — email + heslo, odkaz na obnovu hesla, odkaz na registraci
- **Registrace** — výběr typu (Domácnost / Firma), zadání EAN, email, telefon, ověření SMS, vytvoření hesla
- **Obnova hesla** — 3krokový flow (zadání emailu → email s odkazem → nastavení nového hesla)

### 3.2 Výběr profilu (po přihlášení, před vstupem do portálu)

- Uživatel může mít více rolí a více odběrných míst
- Volí roli (Majitel OM nebo Dodatečný uživatel) a konkrétní odběrné místo
- Po výběru je uživatel přesměrován do autentizované zóny portálu
- **Přepnutí profilu** je možné kdykoli z portálu bez odhlášení prostřednictvím položky „Volba profilu" v postranním menu (sekce Účet)

#### Zobrazení identity v hlavičce portálu

Hlavička portálu zobrazuje dvě nezávislé identity:

| Pozice | Obsah | Příklad |
|---|---|---|
| **Vlevo** (vedle loga) | Zvolený profil — role a identita spravovaného OM | `MAJITEL OM / Jan Novák · Novákova 42` |
| **Vpravo** | Přihlášený uživatel (autor přihlášení) | `Jan Novák` (avatar + jméno) |

> Pokud je přihlášený uživatel zároveň Majitelem OM, jsou obě identity totožné. Liší se v případě Dodatečného uživatele, který spravuje OM jiného zákazníka.

### 3.3 Navigace postranního menu

Postranní menu je strukturováno do sekcí. Pravidla zobrazení:

**Sekce Odběrná místa:**
- Pokud má uživatel **více než jedno OM** → zobrazí se položka **„Přehled OM"** (seznam, z něj proklik na detail)
- Pokud má uživatel **právě jedno OM** → zobrazí se přímo **„Detail OM"** (přímý odkaz na detail)

Cílem je zabránit nejednoznačnosti — uživatel musí vždy vědět, na detail kterého OM odkazuje položka menu.

### 3.4 Autentizovaná zóna — Domácnosti

#### Dashboard
- Přehled aktivních OM (počet, stav)
- Stav posledních žádostí (počet otevřených)
- Notifikace (plánované odstávky, termín odečtu)
- Rychlé akce (Nová žádost, Detail OM, Moje žádosti)

#### Odběrná místa
- **Přehled OM** — seznam odběrných míst uživatele (adresa, EAN, jistič, tarif, stav)
- **Detail OM** — smluvní parametry, EAN, hodnota jističe, typ tarifu, technické parametry měřidla, graf spotřeby (12 měsíců)

#### Potřebuji zařídit
Sekce slouží jako rozcestník dostupných služeb. Každá služba je prezentována jako dlaždice (ikona, název, stručný popis). Proklikem na dlaždici se otevře detail služby.

**Struktura stránky detail služby:**
- Popis služby (co se řeší, kdy je vhodná)
- Číslovaný seznam kroků (jak proces probíhá)
- Přehled potřebných podkladů
- Orientační lhůta vyřízení
- Tlačítko „Přejít k formuláři" (pokud je součástí online formulář)

Dostupné služby — přehled:

| Služba | Typ | Formulář | Lhůta |
|---|---|---|---|
| Změna jističe | Elektro | Ano — online formulář | 30 dní |
| Připojení dobíjecí stanice (EV) | Elektro | Ano — online formulář | 30 dní |
| Připojení k distribuční síti | Elektro | Ano — online formulář | 30 dní |
| Informace o přerušení dodávky | Nastavení | Ano — nastavení notifikací | aktivace do 24 h |
| Změna smlouvy | Smluvní agenda | Ano — online formulář | 30 dní |
| Sdílení elektřiny (CEZ) | Komunitní energetika | Ano — online formulář | 30 dní |
| Samoodečet elektroměru | Přímé zadání | Ano — inline formulář | zpracování do 2 dní |

#### Moje žádosti
- Přehled všech podaných žádostí a jejich stavů
- **Detail žádosti** — časová osa průběhu (přijato → formální kontrola → technická kontrola → rozhodnutí → realizace), přiložené dokumenty

#### Správa uživatelů
- Přidání Dodatečného uživatele (pozvánka na e-mail)
- Nastavení oprávnění (čtení / podávání žádostí)
- Nastavení platnosti přístupu (neomezeně / 3–12 měsíců)
- Odebrání přístupu

#### Nastavení účtu
- Osobní údaje (jméno, e-mail, telefon)
- Změna hesla
- Nastavení notifikací (odstávky, stav žádostí, marketing)

---

## 4. Detailní popis — Přihlášení

### 4.1 Přihlašovací formulář

**Pole:**
- E-mail (typ: email, povinné)
- Heslo (typ: password, povinné, toggle zobrazení hesla)

**Akce:**
- Tlačítko „Přihlásit se"
- Odkaz „Zapomněli jste heslo?" → flow obnovy hesla
- Odkaz „Zaregistrujte se" → registrační flow

**Validace:**
- Validace až po odeslání (ne real-time)
- Chybová hláška vždy obecná: *„Nesprávný e-mail nebo heslo."* (nikdy nespecifikovat, co je špatně)

### 4.2 Bezpečnostní logika — blokování účtu

| Počet neúspěšných pokusů | Akce |
|---|---|
| 1–2 | Zobrazit chybovou hlášku + počet zbývajících pokusů |
| 3 | Dočasné zablokování účtu (délka TBD — viz otevřené otázky) |
| 10 za den | Full lock — nutná obnova hesla |

> Blokování je vázáno na účet, ne na IP adresu.

### 4.3 Flow obnovy hesla

**Krok 1 — Zadání e-mailu**
- Uživatel zadá e-mail
- Systém vždy zobrazí: *„Pokud je e-mail registrován, odeslali jsme instrukce."* (i když e-mail neexistuje — ochrana proti enumeration útoku)

**Krok 2 — E-mail s odkazem**
- Platnost odkazu: 30 minut
- Odkaz je jednorázový (po použití expiruje)
- Možnost „Odeslat znovu": cooldown 60 sekund, max 3 pokusy za hodinu

**Krok 3 — Nastavení nového hesla**
- Pole: Nové heslo + Potvrzení hesla
- Live validace síly hesla:
  - Min. 8 znaků
  - Alespoň jedno velké písmeno
  - Alespoň jedno číslo
  - Alespoň jeden speciální znak
- Po úspěšném uložení → přesměrování na přihlašovací stránku (ne rovnou do portálu)

### 4.4 Otevřené otázky

- [ ] Kolik pokusů a jaká délka dočasného zablokování? *(rozhodnutí: security architekt)*
- [ ] Bude podporováno 2FA (SMS nebo autentikační aplikace)?
- [ ] Jak se chováme při přihlášení neaktivovaného účtu (neověřený telefon)?
- [ ] Bude funkce „zapamatovat si zařízení" / persistent session?

---

## 5. Detailní popis — Registrace

### 5.1 Registrační flow (3 kroky)

**Krok 1 — Zadání údajů**
- Výběr typu zákazníka: Domácnost / Firma (toggle)
- Pole Domácnost: EAN nebo EIC (s nápovědou ⓘ), e-mail, telefonní číslo
- Pole Firma (navíc): IČO
- Tlačítko „Založit" → přechod na SMS ověření

**Krok 2 — Ověření telefonního čísla (SMS)**
- Uživatel zadá 6místný kód zaslaný na zadané telefonní číslo
- Platnost kódu: 10 minut
- Možnost „Odeslat znovu": cooldown 60 sekund, max 3 pokusy za hodinu

**Krok 3 — Vytvoření hesla**
- Pole: Nové heslo + Potvrzení hesla
- Live validace síly hesla (stejná pravidla jako obnova hesla — viz 4.3)
- Tlačítko „Dokončit registraci" → přechod na Výběr profilu

### 5.2 Otevřené otázky

- [ ] Jak ověřujeme, že EAN patří registrujícímu se zákazníkovi? (porovnání s datovým zdrojem?)
- [ ] Jak se chováme, pokud je EAN již přiřazen k jinému účtu?
- [ ] Jaká je lhůta platnosti verifikačního odkazu / kódu po opuštění flow?

---

## 6. Detailní popis — Sekce „Potřebuji zařídit"

### 6.1 Přehled (rozcestník)

Vstupní stránka sekce zobrazuje všechny dostupné služby jako dlaždice (grid, 3 sloupce). Každá dlaždice obsahuje:
- Ikonu služby
- Název služby
- Jednořádkový popis
- Odkaz „Zjistit více →"

### 6.2 Změna jističe *(MVP — plně implementováno)*

**Popis:** Úprava hodnoty hlavního jistícího prvku OM (navýšení nebo snížení). Vhodné při instalaci spotřebičů s vyšším příkonem (tepelné čerpadlo, wallbox, apod.).

**Kroky:**
1. Vyplnění formuláře (odběrné místo, stávající a požadovaná hodnota jističe, důvod)
2. Případné doplnění technické dokumentace na výzvu distributora
3. Technická kontrola proveditelnosti (lhůta 30 dní)
4. Fyzická výměna jistícího prvku technikem distributora
5. Informování e-mailem o výsledku

**Formulář obsahuje:** výběr OM, aktuální jistič (z evidence, read-only), požadovaný jistič (select), důvod (radio: rekonstrukce / nový spotřebič / změna tarifu / jiné), popis, kontaktní údaje.

**Poznámka:** Změna jističe může být zpoplatněna dle platného ceníku.

### 6.3 Připojení dobíjecí stanice pro elektromobil

**Popis:** Souhlas distributora vyžadují dobíjecí stanice s příkonem nad 3,68 kW a veškeré veřejně přístupné nabíjecí body.

> Wallboxy do 3,68 kW (1f, max. 16 A) nevyžadují souhlas distributora.

**Kroky:**
1. Příprava technických parametrů (výkon, typ připojení, model)
2. Podání žádosti o připojení
3. Posouzení kapacity sítě a proveditelnosti (30 dní)
4. Vydání Stanoviska k připojení + případná nová Smlouva o připojení
5. Instalace certifikovaným elektrikářem + revizní zpráva
6. Oznámení o dokončení instalace distributorovi → aktivace

**Poznámka:** Pokud příkon dobíjecí stanice přesahuje stávající jistič, je nutná souběžná žádost o Změnu jističe.

### 6.4 Připojení k distribuční síti

**Popis:** Nové připojení nemovitosti, stavby nebo výrobny k distribuční síti. Týká se také rozšíření stávajícího připojení.

**Kroky:**
1. Příprava: adresa/parcela, požadovaný příkon (kW), typ odběru
2. Podání žádosti o připojení
3. Posouzení technických možností distributorem (30 dní od doložení kompletní žádosti)
4. Vydání Závazného stanoviska + návrh Smlouvy o připojení
5. Realizace přípojky oprávněným elektrikářem dle technických podmínek
6. Žádost o zahájení distribuce a registraci OM

### 6.5 Informace o přerušení dodávky elektřiny

**Popis:** Aktivace zasílání předběžných avíz o plánovaných odstávkách v lokalitě zákazníka.

**Nastavení:**
- Výběr OM (nebo všechna OM)
- Způsob doručení: e-mail / SMS
- Volitelně: upozornění o obnovení dodávky po skončení odstávky

**Pravidla:**
- Notifikace se zasílají minimálně 15 dní před plánovanou odstávkou
- Aktivace do 24 hodin od uložení nastavení
- Nevztahuje se na neplánované výpadky (ty jsou hlášeny přes poruchovou linku 800 400 500)

### 6.6 Změna smlouvy

**Popis:** Změna podmínek Smlouvy o distribuci. Pokrývá tyto typy změn:
- Změna distribuční sazby (tarifu)
- Změna fakturační adresy
- Změna kontaktních údajů (e-mail, telefon)
- Změna způsobu zasílání faktur
- Přepis OM na nového zákazníka (prodej, dědictví)
- Jiná změna smluvních podmínek

**Kroky:**
1. Výběr typu změny
2. Vyplnění formuláře a přiložení dokladů (dle typu)
3. Zpracování distributorem (30 dní)
4. Případná výzva k doplnění informací
5. Potvrzení o provedené změně na e-mail

**Poznámka:** Přepis na nového zákazníka vyžaduje přítomnost obou stran nebo notářsky ověřenou plnou moc.

### 6.7 Sdílení elektřiny (komunitní energetika — CEZ)

**Popis:** Účetní sdílení přebytků elektřiny z vlastní výrobny (FVE, kogenerace) s dalšími členy energetické skupiny. Řídí se zákonem č. 458/2000 Sb. a předpisy ERÚ.

**Podmínky:**
- Aktivní výrobna elektřiny připojená k síti PREdistribuce
- Všechna OM skupiny v distribuční oblasti PREdistribuce, a.s.
- Elektroměr s dálkovým přenosem dat (smart meter)
- Licence ERÚ na výrobu (u výroben nad 10 kW)

**Kroky:**
1. Ověření aktivní výrobny
2. Volba modelu sdílení (bilaterální / komunitní skupina)
3. Podání přihlášky se seznamem EAN kódů všech OM skupiny
4. Posouzení technických podmínek distributorem (30 dní)
5. Podpis Smlouvy o sdílení → aktivace od příštího zúčtovacího období

### 6.8 Samoodečet elektroměru

**Popis:** Přímé zadání stavu elektroměru zákazníkem. Zadaný odečet nahrazuje odhadovanou spotřebu ve vyúčtování.

**Formulář:**
- Výběr OM
- Datum odečtu (předvyplněno aktuálním datem)
- Hodnota VT (hlavní sazba, kWh) — vždy
- Hodnota NT (nízká sazba, kWh) — jen u dvousazbových tarifů

**Pravidla:**
- Zadaná hodnota musí být vyšší než poslední zaznamenaný odečet
- Odečet lze zadávat zpravidla v předepsaném termínovém okně (poslední týden měsíce)
- Zpracování do 2 pracovních dní
- OM se smart meterem se odečítají automaticky — samoodečet není povinný

---

## 7. Technický stack (návrh)

| Vrstva | Technologie |
|---|---|
| Frontend | Next.js + Tailwind CSS |
| Backend / Auth / DB | Supabase (PostgreSQL + Auth) |
| Verzování | GitHub |
| Hosting | Vercel |

---

## 8. MVP scope — co je IN a co je OUT

### IN (první release)

**Autentizace a správa účtu:**
- Registrace a přihlášení (domácnosti)
- Obnova hesla (3krokový flow)
- Výběr profilu / role + odběrného místa
- Přepnutí profilu z portálu bez odhlášení
- Nastavení účtu (osobní údaje, heslo, notifikace)
- Správa Dodatečného uživatele (pozvánka, oprávnění, odebrání)

**Odběrná místa:**
- Přehled OM + Detail OM (smluvní a technické parametry, graf spotřeby)
- Podmíněná navigace: Přehled OM (2+ OM) vs. Detail OM (1 OM)

**Potřebuji zařídit (všechny 4 typy interakcí):**
- Změna jističe — online formulář + sledování stavu
- Připojení dobíjecí stanice (EV) — online formulář
- Připojení k distribuční síti — online formulář
- Informace o přerušení dodávky — nastavení notifikací
- Změna smlouvy — online formulář
- Sdílení elektřiny (CEZ) — online formulář
- Samoodečet elektroměru — inline formulář

**Moje žádosti:**
- Přehled žádostí + Detail žádosti (časová osa, dokumenty)

### OUT (roadmapa)

- Firmy jako typ zákazníka
- FVE žádosti (připojení FVE, navýšení výkonu, bateriové úložiště)
- Odečty — historie, přehled dálkových přenosů
- Poruchy a odstávky — hlášení poruch, mapa výpadků
- Dokumenty a smlouvy — archiv vydaných dokumentů
- Komunikační inbox — zprávy a odpovědi k žádostem
- 2FA (SMS nebo autentikační aplikace)
- Nápověda a podpora — FAQ, chat

---

*Dokument je živý — bude průběžně doplňován.*
