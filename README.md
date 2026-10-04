# deutch

Sbírka statických vzdělávacích webových aplikací pro žáky základní školy.
Hostováno zdarma na **Cloudflare Pages**, automatický deploy při push na `main`.

Produkční URL: **https://deutch.krupa.link/**

## Struktura repozitáře

Každá appka je samostatná složka v kořeni repa se svým vlastním `index.html`
(čistý statický web — HTML/CSS/JS, žádný build krok je potřeba, pokud appka
sama nevyžaduje bundler).

```
deutch/
├── index.html          ← rozcestník se seznamem všech appek
├── apps.json           ← seznam appek, ze kterého se rozcestník generuje
├── _headers             ← Cloudflare Pages hlavičky (cache, security)
├── slovicka-zvirata/    ← ukázková appka
│   └── index.html
└── ...
```

Výsledná URL appky: `https://deutch.krupa.link/<nazev-slozky>/`

## Jak přidat novou appku

1. Vytvoř novou složku v kořeni repa, např. `cislovky/`.
2. Dovnitř dej samostatný `index.html` (+ případně `style.css`, `script.js`,
   obrázky atd.) — appka musí fungovat čistě staticky, bez serveru.
3. Přidej appku do `apps.json` (název, popis, cesta) — rozcestník na hlavní
   stránce se podle toho sám vykreslí.
4. Commitni a pushni na `main` větev. Cloudflare Pages appku automaticky
   nasadí do pár desítek sekund.

## Lokální test appky

Appky jsou čistě statické, takže stačí spustit libovolný statický server
v kořeni repa, např.:

```bash
python3 -m http.server 8000
```

a appku otevřít na `http://localhost:8000/<nazev-slozky>/`.

## Nasazení (Cloudflare Pages)

Repo je napojené na Cloudflare Pages projekt s automatickým deployem:

- **Production branch:** `main`
- **Build command:** (žádný — statický web)
- **Build output directory:** `/` (kořen repa)
- **Custom domain:** `deutch.krupa.link`

Každý push na `main` spustí nový deploy; pull requesty dostanou vlastní
preview URL (`<hash>.deutch.pages.dev`).
