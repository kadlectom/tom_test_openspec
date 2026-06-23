## Context

PREdistribuce365 je nový zákaznický portál pro domácnosti v distribuční oblasti PREdistribuce, a.s. Portál řeší rostoucí poptávku po samoobslužném řešení pro správu odběrných míst a podávání žádostí bez nutnosti osobního či telefonického kontaktu. MVP se zaměřuje výhradně na segment Domácností.

Cílová skupina:
- Majitelé odběrných míst (Majitel OM)
- Osoby pověřené správou (Dodatečný uživatel)

Geografický rozsah: Distribuční oblast PREdistribuce, a.s.

## Goals / Non-Goals

**Goals:**

- Umožnit domácnostem bezpečně se registrovat, přihlásit a spravovat více odběrných míst
- Poskytnout intuitivní rozcestník služeb s online formuláři pro 7 typů distribuničních služeb
- Umožnit sledování stavu podaných žádostí v reálném čase
- Zautomatizovat správu uživatelů a rolí (pozvánky, oprávnění, deaktivace)
- Poskytnout design systém odpovídající brandingu PREdistribuce s primární barvou tmavě modrou (#1a2f6e)

**Non-Goals:**

- Není součástí MVP podpora Firem jako typu zákazníka
- FVE žádosti (připojení FVE, navýšení výkonu bateriových úložišť)
- 2FA (SMS nebo aplikace) — je v roadmapě
- Komunikační inbox a live chat se zákazníkem
- Integrace s externími systémy (zatím pouze API endpoint)

## Decisions

### 1. Tech Stack: Next.js + Tailwind + Supabase

**Rationale:** Next.js poskytuje server-side rendering (SEO, performance) a API routes pro komunikaci s backendem. Tailwind CSS akceleruje stylování a zaručuje konzistenci. Supabase (PostgreSQL + Auth) eliminuje nutnost vlastního auth serveru a zajišťuje GDPR compliance.

**Alternatives Considered:**
- React + Node.js (Express) — vyžaduje více setup, vyšší ops overhead
- Vue.js — méně sjednocený ekosystem pro corporate aplikace
- Firebase — méně kontroly nad daty (vendor lock-in)

### 2. Dvousloupcový Layout pro Auth Pages

**Rationale:** Levý sloupec (55%) formulář, pravý sloupec (45%) benefits/informace. Tímto vzorem se maximalizuje konverze registrace a poskytuje prostor pro marketing messaging. Tmavě modrý pravý panel vytváří silnou vizuální hierarchii.

**Alternatives Considered:**
- Jednosloupcový layout — jednodušší responsive, ale méně důstojný vzhled
- Fullscreen formulář — lepší pro mobile, ale horší pro desktop (40% plochy nevyužitá)

### 3. SMS-Based Account Verification (ne email)

**Rationale:** SMS ověření během registrace zajišťuje, že uživatel má reálný telefonní kontakt. Kombinace EAN ověření (z datových zdrojů PREdistribuce) + SMS výrazně snižuje fraud a fake registrace. Email se používá pouze pro obnovu hesla.

**Alternatives Considered:**
- Email ověření — méně bezpečné, vyšší fraud
- Bez ověření — není přijatelné pro energetiku

### 4. Nový OM Detail (read-only + Výběr profilu bez odhlášení)

**Rationale:** Detail OM se zobrazuje v levém sloupci, pravý panel fixní (benefit messages). Přepínání profilu je dostupné z navigace bez odhlášení — to zvyšuje UX. Profil "Dodatečný uživatel" vidí pouze OM, na které má přístup.

**Alternatives Considered:**
- Vždy zobrazit "Přehled OM" seznam — zbytečný klik pro uživatele s 1 OM
- Vyžadovat odhlášení pro přepnutí profilu — horší UX

### 5. Online Formuláře vs. E-signed Documents

**Rationale:** Všechny žádosti jsou online formuláře (validace, workflow). Pokud je nutný digitální podpis, systém stahuje dokument pro podepsání externími tools (Docusign, etc.). Tímto se zjednodušuje backend a odsouvá se compliance na specialisovaný vendor.

**Alternatives Considered:**
- Lokální podpisy v aplikaci — vyšší compliance risk
- PDF dokumenty bez podpisů — nesplňuje právní nároky

### 6. Status Tracking bez Real-time Websockets

**Rationale:** Stav žádostí se aktualizuje pull-based (user klikne, system fetches status). Pro MVP je dostatečné, snižuje ops complexity. Real-time notifikace (push notifications) jsou v roadmapě.

**Alternatives Considered:**
- WebSocket + Redis — vyšší infrastruktura, pre-mature optimizace

### 7. Modulární Spec Structure

**Rationale:** Každý capability má svůj spec soubor (`specs/<capability>/spec.md`), což umožňuje granulární aktualizaci bez ovlivnění ostatních. Lehčí pro delta management v budoucnu.

## Risks / Trade-offs

| Risk | Mitigation |
|---|---|
| **Rate limiting** — Formuláře bez rate limitingu na backend | Implementovat leaky bucket algorithm na API endpoint; omezit submits na 1x za 5 sekund |
| **Account lockout** — Uživatelé zapomínají hesla a lockují si účty | Provide reset hesla bez lockoutu; monitoring lockoutu, alerting po 10+ pokusech/den |
| **EAN validation** — Ověření EAN ze zdroje dat bude offline/pomalý | Cache EAN data s weekly sync; fallback na manuální ověření PREdistribuce |
| **GDPR compliance** — Zachování osobních dat | Implementovat audit logs; anonymizace starých dat po 3 letech; encryption at rest |
| **Performance** — Stránka s grafem 12 měsíců spotřeby | Lazy load grafy; agregace dat (týdenní agregace místo denní); CDN caching |
| **Mobile responsiveness** — Dvousloupcový layout na mobilu | Responsive design: pravý panel se skrývá na <768px; formulář full width |

## Migration Plan

**Phase 1 (Week 1-2): Backend Setup**
- Provisioning Supabase (PostgreSQL schema, auth setup)
- API endpoints pro auth, OM, žádosti
- EAN data import z externího zdroje
- Testing auth flows (happy path + edge cases)

**Phase 2 (Week 3-4): Frontend Scaffolding**
- Vytvoření Next.js projektu, Tailwind setup
- Design system komponenty (button, input, card, etc.)
- Layout struktura (header, footer, sidebar, main content)
- Integrace Supabase auth SDK

**Phase 3 (Week 5-6): Core Features**
- Registrace + SMS ověření
- Přihlášení + Obnova hesla
- Výběr profilu + OM overview/detail
- Sidebar navigace s rolí-specific items

**Phase 4 (Week 7-8): Service Requests**
- Formuláře pro 7 služeb (Změna jističe, EV, Připojení, Notifikace, Smlouva, Sdílení, Samoodečet)
- File upload pro přílohy
- Validace formuláře (client-side + server-side)

**Phase 5 (Week 9-10): Status Tracking**
- Žádosti přehled + Detail s timeline
- Status badges (Přijato, Validace, Rozhodnutí, Realizace)
- Document viewer pro přílohy

**Phase 6 (Week 11-12): Account Management + QA**
- Správa dodatečných uživatelů (pozvánky, oprávnění)
- Nastavení notifikací
- Responsive testing
- Security audit (SQL injection, XSS, CSRF)
- Load testing

**Rollout:** Vercel deployment s blue-green strategy. Rollback: Git revert + Vercel rollback (< 5 minut).

## Open Questions

- [ ] Jak dlouho trvá validace EAN z externího zdroje? Je synchronní nebo asynchronní?
- [ ] Jaký je SLA pro odpověď distributora na žádost (30 dní je lhůta, ale kdy začíná běžet)?
- [ ] Budou mít uživatelé viditelný status "Čeká na dodatečné podklady" nebo jen "V procesu"?
- [ ] Je nutný audit log všech akcí uživatele (GDPR)?
- [ ] Jaké jsou limity na počet Dodatečných uživatelů na OM?
- [ ] Integrace payment gateway pro eventuální zpoplatnění služeb v budoucnu?
