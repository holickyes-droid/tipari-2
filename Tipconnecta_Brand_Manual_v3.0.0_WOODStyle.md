# Tipconnecta Brand Manual
Design system & guidelines platformy – **WOOD-style (Deep Teal + Rich Red)**

> Poznámka k přesnosti barev: HEX hodnoty níže jsou **odvozené z veřejných materiálů WOOD (a vašich screenshotů)**. Pro finální implementaci doporučujeme ověřit finální odstíny v dodaných brand assetech / CSS.

---

## Obsah
1. Filozofie  
2. Barvy  
3. Typografie  
4. Layout & Spacing  
5. Buttons  
6. Forms  
7. Tabulky  
8. Ikony  
9. Modals & Drawers  
10. Badges & Alerts  
11. Loading States  
12. Accessibility  
13. Copywriting  
14. Do's & Don'ts  
15. Version

---

## Version
**3.0.0** · React + Tailwind v4  
Vizuální směr: **Premium investment portal / „client portal“** (WOOD-style)

---

## 1) Filozofie designu
Cílem je převést Tipconnecta UI do vizuálního jazyka typu **investment bank / wealth management portál**: **tmavý zelenomodrý (teal) „canvas“**, na něm **bílé karty**, s akčním **bohatým červeným** akcentem.

WOOD ve veřejném popisu identity pracuje s „**modified green**“ a „**rich red**“ (moderní energie) a moderním groteskem pro logotyp. citeturn6view0  
V Tipconnecta to překlápíme do pravidel pro UI, ne do kopie brandu.

### 3 klíčové hodnoty
- **Důvěra & stabilita**: vysoký kontrast, konzervativní typografie, minimální ornament.  
- **Kontrola & přehled**: karty a tabulky jsou dominantní, čísla mají prioritu.  
- **Prémiovost**: tmavý teal background + velké radiusy + čisté bílé plochy.

### Atmosféra
Formální, konzervativní, „investment-grade“. Odvážnost jen v akcentní červené a v kontrastu.

---

## 2) Barevná paleta

### Primary (Teal) – „WOOD Green / Deep Teal“
Použití: background canvas, selected states, focus ring, linky v UI, sekundární CTA.

| Token | HEX | Tailwind návrh |
|---|---:|---|
| tc-teal-50 | #E9F6F5 | bg-tc-teal-50 |
| tc-teal-100 | #D2EEEB | bg-tc-teal-100 |
| tc-teal-200 | #A7DCD7 | bg-tc-teal-200 |
| tc-teal-300 | #7CCAC3 | bg-tc-teal-300 |
| tc-teal-400 | #4FB5AD | bg-tc-teal-400 |
| tc-teal-500 | #2D9A93 | bg-tc-teal-500 |
| tc-teal-600 | #136C66 | bg-tc-teal-600 |
| tc-teal-700 | #0E524F | bg-tc-teal-700 |
| tc-teal-800 | #083B38 | bg-tc-teal-800 |
| tc-teal-900 | #062018 | bg-tc-teal-900 |
| tc-teal-950 | #051D1B | bg-tc-teal-950 |

**App background (default):**
- `bg-tc-teal-900` nebo gradient:  
  `bg-[radial-gradient(1200px_circle_at_20%_-10%,#136C66_0%,#0E524F_35%,#051D1B_100%)]`

### Secondary / Accent (Rich Red) – „WOOD Red“
Použití: primární CTA, zvýraznění „Next/Action“, ikonové akcenty.

| Token | HEX | Tailwind návrh |
|---|---:|---|
| tc-red-50 | #FFF3F1 | bg-tc-red-50 |
| tc-red-100 | #FFE1DD | bg-tc-red-100 |
| tc-red-200 | #FFC2BA | bg-tc-red-200 |
| tc-red-300 | #FFA091 | bg-tc-red-300 |
| tc-red-400 | #F47F71 | bg-tc-red-400 |
| tc-red-500 | #EB695B | bg-tc-red-500 |
| tc-red-600 | #C85046 | bg-tc-red-600 |
| tc-red-700 | #B6473E | bg-tc-red-700 |
| tc-red-800 | #9A3C35 | bg-tc-red-800 |
| tc-red-900 | #7D302B | bg-tc-red-900 |

> **A11y poznámka:** `tc-red-500` má na white často jen ~3:1 kontrast pro white text, proto pro **filled button s bílým textem** používáme minimálně `tc-red-600`.

### Neutrals (Ink/Paper)
Použití: texty, card background, borders.

- **Canvas text on teal:** `text-white`, `text-white/80`, `text-white/60`
- **Card background:** `bg-white`
- **Card muted background:** `bg-slate-50` (nebo `bg-white/80` pro jemný „frosted“ look)
- **Borders:** `border-slate-200` (na bílé), `border-white/10` (na tealu)
- **Text – headings:** `text-slate-900`
- **Text – body:** `text-slate-700`
- **Text – meta:** `text-slate-500`

### Status colors (odděleně od brand red)
Status barvy držíme konzistentně a **nepoužíváme brand red** jako error.

- **Success:** `emerald-600` (#059669)  
- **Warning:** `amber-500` (#F59E0B)  
- **Error:** `red-600` (#DC2626)  
- **Info:** `sky-600` (#0284C7)

---

## 3) Typografie

### Font family
- **Primární:** Inter (UI-safe, čitelnost tabulek)  
- **Fallback:** system-ui, -apple-system, Segoe UI, Roboto, sans-serif  
- (Volitelné pro „WOOD vibe“): pro nadpisy lze zvážit moderní grotesk (licence), ale MVP drží Inter.

### Kritické pravidlo pro finanční data
- VŽDY: `tabular-nums` pro částky, procenta, data, ID.

### Type scale (Tailwind)
H1 – Page title  
- `text-3xl font-semibold tracking-tight text-slate-900`

H2 – Section  
- `text-xl font-semibold text-slate-900`

H3 – Card title  
- `text-lg font-semibold text-slate-900`

Body  
- `text-base text-slate-700 leading-6`

Caption / Meta  
- `text-sm text-slate-500`

Čísla (v kartách / KPI)
- `text-2xl font-semibold tabular-nums text-slate-900`

---

## 4) Layout & Spacing

### Základní grid
- Desktop container: `max-w-[1200px]` až `max-w-[1320px]` dle obrazovky
- Stránka na tealu: content vždy v „white card“ kontejnerech (čitelnost)

### Border radius (WOOD-style = větší radius)
- **Buttons, inputs:** `rounded-full` (pill) nebo `rounded-2xl` (16px) podle komponenty
- **Cards (default):** `rounded-3xl` (24px)
- **Modals / drawers:** `rounded-3xl` (24px)

### Shadows (na tmavém canvasu jemně)
- Cards: `shadow-sm` (default), `shadow-md` (elevated)
- Modals: `shadow-lg`
- Popovers: `shadow-lg`

### Padding
- Card header: `p-6` (24px)
- Card content: `p-6` (24px) / `p-8` (32px) pro „hero“ karty
- Buttons: `px-5 py-2.5` (default), `px-6 py-3` (large)

### Whitespace
- Vysoký whitespace: **ANO**
- Density: **medium-low** (B2B data → stále přehledné tabulky)

---

## 5) Buttons

### Primary (Brand CTA = Rich Red)
Použití: 1 hlavní akce na kontext (submit, vytvořit, potvrdit).

**Class recipe:**
- `bg-tc-red-600 hover:bg-tc-red-700 text-white`
- `rounded-full px-5 py-2.5 font-semibold`
- `focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-tc-teal-300 focus-visible:ring-offset-2 focus-visible:ring-offset-white`

### Secondary (Teal outline / white fill)
Použití: vedlejší akce.

- `bg-white text-tc-teal-800 border border-tc-teal-200 hover:bg-tc-teal-50`
- `rounded-full px-5 py-2.5 font-semibold`

### Ghost
- `bg-transparent text-tc-teal-100 hover:bg-white/10`
- (na bílých kartách) `text-tc-teal-800 hover:bg-tc-teal-50`

### Destructive (status error red)
- `bg-red-600 hover:bg-red-700 text-white`
- vždy confirm modal

**Pravidlo:** Max. 1 primary button v jednom kontextu.

---

## 6) Forms (Inputs)

### Input (na bílé kartě)
- Border: `border border-slate-200`
- Background: `bg-white`
- Text: `text-slate-900 placeholder:text-slate-400`
- Radius: `rounded-2xl` nebo `rounded-full` (dle komponenty)
- Height: `h-11`
- Focus: `focus-visible:ring-2 focus-visible:ring-tc-teal-300 focus-visible:border-tc-teal-300`

### Validace
- Error text: `text-sm text-red-600`
- Error border: `border-red-300` + ring `ring-red-200`

Používáme `react-hook-form + zod`.

---

## 7) Tabulky

### Design pravidla
Table vždy uvnitř bílé karty:

- Header row:
  - Background: `bg-slate-50`
  - Text: `text-xs font-semibold text-slate-500 uppercase tracking-wide`
  - Border: `border-b border-slate-200`
- Rows:
  - Text: `text-sm text-slate-900`
  - Hover: `hover:bg-slate-50`
  - Padding: `px-4 py-3`
- Číselné sloupce:
  - `text-right tabular-nums`

Stripe: `even:bg-slate-50` (volitelně)

---

## 8) Ikony
- Knihovna: `lucide-react` (MVP standard)
- Styl: outline
- Velikosti: 16 / 20 / 24 (h-4, h-5, h-6)
- Stroke: default `1.5` (na tmavém canvasu může být čitelnější `1.75–2`)

Icon-only buttony: povinné `aria-label` nebo `sr-only`.

---

## 9) Modals & Drawers

### Modal (Dialog)
- Overlay: `bg-black/60`
- Container: `bg-white rounded-3xl shadow-lg`
- Width: `max-w-lg` (standard)
- Padding: `p-8`

### Drawer (Sheet)
- Right: `fixed right-0 top-0 h-full w-[480px] bg-white shadow-lg`
- Bottom (mobile): `fixed bottom-0 left-0 right-0 rounded-t-3xl`

Best practices:
- Close button (X)
- ESC zavírá
- Klik mimo zavírá (kromě destructive)

---

## 10) Badges & Alerts

### Badges
- Pill: `rounded-full px-3 py-1 text-xs font-semibold`
- Default: `bg-slate-100 text-slate-700`
- Teal: `bg-tc-teal-100 text-tc-teal-800`
- Red accent: `bg-tc-red-100 text-tc-red-800`
- Warning: `bg-amber-100 text-amber-800`
- Error: `bg-red-100 text-red-800`

### Alerts
- Success: `bg-emerald-50 border-emerald-200 text-emerald-900`
- Warning: `bg-amber-50 border-amber-200 text-amber-900`
- Error: `bg-red-50 border-red-200 text-red-900`
- Info: `bg-sky-50 border-sky-200 text-sky-900`

---

## 11) Loading states
- Skeleton: `animate-pulse bg-slate-100`
- Spinner: `text-tc-teal-300` (na tealu) / `text-tc-teal-700` (na bílé)
- Toast: Sonner (beze změny)

---

## 12) Accessibility (a11y)
- Focus ring: vždy `focus-visible:ring-2` (primárně teal)
- Klávesnice: TAB order, ESC modals, ENTER submit
- Nejen barva: status vždy doplnit ikonou + textem
- Kontrast: na tealu používat `text-white` nebo `text-white/80`

---

## 13) Copywriting & Voice
- Jazyk: CZ (výhradně)
- Tón: formální vykání, profesionální, bez marketingu
- V UI vždy: „co to znamená“ + „co je další krok“

Buttony: Sloveso + objekt  
- „Odeslat žádost“, „Podepsat smlouvu“, „Potvrdit financování“

Error: Co se stalo + co udělat  
- „Nepodařilo se uložit změny. Zkuste to znovu, nebo kontaktujte podporu.“

Empty: Proč je prázdné + CTA  
- „Zatím zde nejsou žádná data.“ + „Vytvořit…“

---

## 14) Do's & Don'ts

### DO ✓
- Používej **tmavý teal canvas + bílé karty**
- Primární CTA dělej **rich red**, secondary **teal**
- `tabular-nums` všude pro čísla
- Velké radiusy (`rounded-3xl` pro karty, `rounded-full` pro buttony)
- Jemné shadow (na tealu)

### DON'T ✗
- Nepoužívej původní „Primary Blue“ jako hlavní akcent
- Nepoužívej brand red pro error stavy
- Nepřeháněj gradienty uvnitř komponent (gradient patří na pozadí/hero)
- Nedávej více než 1 primary CTA na kontext
- Nezhušťuj tabulky tak, že se zhorší čitelnost

---
