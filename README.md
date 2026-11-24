# Página de download do AbigailOvos

Site estático de download do AbigailOvos. **Este é um projecto separado do projecto original** (`Denilson-Marrengula/AbigailOvos`): a app e a release do APK ficam no repo original; esta página apenas aponta para o ficheiro publicado nessa release.

A estrutura visual foi inspirada na página "Entrega Já"; a identidade visual vem da APK.

## Identidade visual

- Cores lidas de `mobile/lib/design/app_theme.dart`:
  - verde floresta `#134937`
  - dourado `#D9B956`
  - creme `#FAF9F2`
- Logótipo: `assets/logo.png` (cópia de `mobile/assets/logo.png`).
- Favicon: `assets/favicon.png` (cópia de `mobile/web/favicon.png`).
- Ícone Apple Touch: `assets/apple-touch-icon.png` (cópia de `mobile/web/icons/Icon-192.png`).

Não usar as cores nem o SVG da página de referência.

## Estrutura desta pasta

```text
index.html        página pública (com os marcadores abaixo)
assets/           logótipo, favicon e apple-touch-icon
README.md         este ficheiro
app-debug.apk     cópia local de referência — NÃO publicar no repo do site
```

## O que falta substituir antes de publicar

O `index.html` tem dois marcadores que **têm de ser substituídos**:

- `COLOCA_AQUI_A_URL_DO_DOWNLOAD` — URL do APK publicado na release (linha ~241).
- `COLOCA_AQUI_A_URL_DA_PAGINA` — URL pública final desta página (linha ~24, `og:url`).

Nenhum segredo deve ser colocado nesta página.

## Por que o APK não vai para o GitHub Pages nem para o repo do site

O APK tem cerca de **181 MB**. O GitHub bloqueia ficheiros com mais de **100 MB** num repositório, e o GitHub Pages serve apenas ficheiros do repo. Por isso o APK fica como **asset de uma GitHub Release** no repo original, e esta página só aponta para lá.

```text
Ficheiro:  app-debug.apk (181 025 134 bytes)
SHA-256:  56FDCCA6A1599F64107453C2BC7BCACB7E5903230D2956CC5758D7AB9354DD6D
```

## Passo 1 — Publicar o APK no repo original

1. Abrir: https://github.com/Denilson-Marrengula/AbigailOvos/releases/new
2. Criar a tag `v1.0.0` (**“Create a new tag on publish”**), com target `main`.
3. Título: `AbigailOvos v1.0.0 (debug)`. Incluir na descrição o SHA‑256 acima e o aviso de que é uma APK debug.
4. Anexar como asset o ficheiro `artifacts/app-debug.apk` do repo original. O upload pode demorar alguns minutos; se falhar no browser, usar `gh release upload v1.0.0 <ficheiro>`.
5. Clicar em **Publish release**.
6. Copiar a URL de download do asset (clique direito no nome do ficheiro → copiar ligação). Formato esperado:

```text
https://github.com/Denilson-Marrengula/AbigailOvos/releases/download/v1.0.0/AbigailOvos-debug.apk
```

Se o ficheiro for anexado sem renomear, a URL termina em `/app-debug.apk`. **Não** usar a URL da página da release nem `/releases/latest`.

## Passo 2 — Publicar esta página num repo novo

1. Criar no GitHub o repositório público `Denilson-Marrengula/AbigailOvosSite` (sem ficheiros iniciais).
2. Nesta pasta, iniciar o Git e ligar o remote:

```powershell
cd C:\Users\HP\Documents\NetBeansProjects\AbigalOvosSite
git init -b main
git remote add origin https://github.com/Denilson-Marrengula/AbigailOvosSite.git
```

3. Criar `.gitignore` **antes** de qualquer `git add`, para o APK de 181 MB não entrar no repo:

```powershell
@"
*.apk
app-debug.apk
"@ | Set-Content .gitignore
```

4. Substituir os dois marcadores em `index.html`:
   - download → a URL do Passo 1;
   - `og:url` → `https://denilson-marrengula.github.io/AbigailOvosSite/`.

5. Enviar o site (evitar `git add .`):

```powershell
git add .gitignore index.html assets README.md
git commit -m "Página de download do AbigailOvos"
git push -u origin main
```

6. Activar GitHub Pages no repo `AbigailOvosSite`: **Settings → Pages → Source: Deploy from a branch → `main` → `/ (root)` → Save**.  
   A pasta é a raiz do repo, **não** `/download`.

7. URL final da página:

```text
https://denilson-marrengula.github.io/AbigailOvosSite/
```

Se o nome do repo for outro, trocar `AbigailOvosSite` pela nome escolhido na URL.

8. Confirmar no telemóvel que o botão descarrega o APK e que o Android instala (será necessário permitir instalação de fontes desconhecidas).

## Nota

Esta é uma APK **debug**, assinada com a chave de depuração. Para distribuição real, gerar uma release com keystore própria, actualizar o asset da release, a URL e o hash, e actualizar esta página.
