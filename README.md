# dev-garden-portfolio

> 🇧🇷 [Leia em Português (pt-BR)](./README-pt-br.md)

Felipe Vandevelde's portfolio and digital garden, live at [dev-garden-portfolio.vercel.app](https://dev-garden-portfolio.vercel.app).

It is built from the [dev-garden](https://github.com/FelipeVandevelde/dev-garden) template. Setup, commands, environment variables, note syntax and deployment are documented in the [template's README](https://github.com/FelipeVandevelde/dev-garden#readme); this file only covers what is specific to this copy.

## How this site is set up

- **Hosting:** Vercel builds `main`.
- **Notes:** they come from the Obsidian vault in `FelipeVandevelde/vault-obsidian`. Vercel sets `VAULT_REPO` to that repository and `USE_REMOTE_VAULT=true`. A GitHub Action in the vault calls a Vercel Deploy Hook on every push to `main`, so a new note triggers a rebuild.
- **Personal files:** `src/site.config.ts`, `src/content/profile/`, `README.md` and `README-pt-br.md`. Everything else stays the same as the template.

## Run locally

```bash
npm install
cp .env.example .env
npm run dev
```

The default `.env` reads the template's `sample-vault/`. To see the real notes, set `VAULT_REPO=FelipeVandevelde/vault-obsidian`, `USE_REMOTE_VAULT=true` and a `GH_PAT`, or point `LOCAL_VAULT_PATH` at a local clone of the vault.

The end-to-end tests expect the sample vault: build with `LOCAL_VAULT_PATH=sample-vault USE_REMOTE_VAULT=false npm run build`, then run `npx playwright test`.

## Pulling template updates

Code and doc changes go into `dev-garden` first and reach this repository through the `upstream` remote. On a branch off `dev`:

```bash
git fetch upstream
git merge upstream/main
```

If a personal file conflicts, keep this repository's version:

```bash
git checkout HEAD -- src/content/profile src/site.config.ts README.md README-pt-br.md
git commit
```

`src/site.config.ts` also holds the config schema, so check that only values differ from the template afterwards, and copy any schema change over by hand:

```bash
git diff upstream/main -- src/site.config.ts
```

Then merge into `dev` and open a pull request to `main`. When the copy is up to date, `git log HEAD..upstream/main` prints nothing, and `git diff --stat upstream/main` lists only the personal files.

## License

[MIT](./LICENSE)
