## Why

Distributor elektrické energie PREdistribuce potřebuje nový samoobslužný zákaznický portál, který umožní domácnostem spravovat svá odběrná místa, podávat žádosti o distribuční služby a komunikovat s distributorem bez nutnosti telefonického či osobního kontaktu. Cílem MVP je automatizovat běžné procesy a zlepšit zákaznickou zkušenost.

## What Changes

Nový portál **PREdistribuce365** bude zahrnovat:

- Bezpečná autentizace a správa uživatelských účtů (registrace, přihlášení, obnova hesla)
- Systém rolí (Majitel OM, Dodatečný uživatel) a přepínání mezi více odběrnými místy
- Přehled a detaily odběrných míst s technickými parametry a grafem spotřeby
- Rozcestník služeb s online formuláři pro podání žádostí:
  - Změna jističe
  - Připojení dobíjecí stanice (EV)
  - Připojení k distribuční síti
  - Informace o přerušení dodávky
  - Změna smlouvy
  - Sdílení elektřiny (komunitní energetika)
  - Samoodečet elektroměru
- Sledování stavu podaných žádostí (časová osa, dokumenty)
- Správa Dodatečných uživatelů s granulárními oprávněními
- Nastavení notifikací a osobních údajů

## Capabilities

### New Capabilities

- `customer-portal-ui`: Responsivní webový portál s dvousloupcovým designem (levý sloupec obsah, pravý sloupec benefits/info)
- `user-authentication`: Registrace (EAN ověření, SMS kód), přihlášení (email + heslo), obnova hesla (3krokový flow), blokování účtu
- `profile-management`: Výběr a přepínání profilu, správa rolí (Majitel OM, Dodatečný uživatel), správa dodatečných uživatelů s pozvánkami
- `metering-points-overview`: Přehled všech odběrných míst s EAN, adresou, jističem, tarifem a stavem
- `metering-points-detail`: Detail OM s technickými parametry (typ měřidla, graf spotřeby za 12 měsíců), smluvními údaji
- `service-request-forms`: Online formuláře pro podání 7 typů distribuničních služeb (změna jističe, EV nabíjení, připojení, notifikace, změna smlouvy, sdílení elektřiny, samoodečet)
- `request-tracking`: Přehled podaných žádostí s filtry, detail žádosti s časovou osou (přijato → validace → rozhodnutí → realizace) a přiloženými dokumenty
- `account-settings`: Správa osobních údajů, změna hesla, nastavení notifikací (odstávky, stav žádostí), dashboard se shrnutím
- `design-system-predistribuce`: UI komponenty, barevná paleta (tmavě modrá #1a2f6e, červená #e30613, zelená #5a7a2b), typografie, Button primární/sekundární, textové inputy, chybové hlášky

### Modified Capabilities

- (Žádné modifikace existujících capabilit - jedná se zcela o nový projekt)

## Impact

- Frontend: Next.js + Tailwind CSS
- Backend/Auth/DB: Supabase (PostgreSQL + autentizace)
- Hosting: Vercel
- Verzování: GitHub
- Design: Custom design systém (PRE barevná paleta, specifické komponenty)
- Bezpečnost: Blokování účtu po neúspěšných pokusech, obrana proti enumeration útokům, minimálně 30 minut platnost reset tokenů
