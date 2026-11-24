# dev-garden-portfolio

> 🇺🇸 [Read in English](./README.md)

Portfólio e jardim digital de Felipe Vandevelde, no ar em [dev-garden-portfolio.vercel.app](https://dev-garden-portfolio.vercel.app).

Ele é feito a partir do template [dev-garden](https://github.com/FelipeVandevelde/dev-garden). Instalação, comandos, variáveis de ambiente, sintaxe das notas e deploy estão no [README do template](https://github.com/FelipeVandevelde/dev-garden/blob/main/README-pt-br.md); este arquivo cobre só o que é específico desta cópia.

## Como este site está configurado

- **Hospedagem:** a Vercel gera o build da `main`.
- **Notas:** vêm do vault do Obsidian em `FelipeVandevelde/vault-obsidian`. Na Vercel, `VAULT_REPO` aponta para esse repositório e `USE_REMOTE_VAULT=true`. Uma GitHub Action no vault chama um Deploy Hook da Vercel a cada push na `main`, então uma nota nova dispara um novo build.
- **Arquivos pessoais:** `src/site.config.ts`, `src/content/profile/`, `README.md` e `README-pt-br.md`. Todo o resto fica igual ao template.

## Rodando localmente

```bash
npm install
cp .env.example .env
npm run dev
```

O `.env` padrão lê o `sample-vault/` do template. Para ver as notas reais, defina `VAULT_REPO=FelipeVandevelde/vault-obsidian`, `USE_REMOTE_VAULT=true` e um `GH_PAT`, ou aponte `LOCAL_VAULT_PATH` para um clone local do vault.

Os testes end-to-end esperam o vault de exemplo: gere o build com `LOCAL_VAULT_PATH=sample-vault USE_REMOTE_VAULT=false npm run build` e depois rode `npx playwright test`.

## Trazendo atualizações do template

Mudanças de código e de documentação entram primeiro no `dev-garden` e chegam a este repositório pelo remote `upstream`. Numa branch criada a partir da `dev`:

```bash
git fetch upstream
git merge upstream/main
```

Se um arquivo pessoal entrar em conflito, mantenha a versão deste repositório:

```bash
git checkout HEAD -- src/content/profile src/site.config.ts README.md README-pt-br.md
git commit
```

O `src/site.config.ts` também guarda o schema da configuração, então confira depois que só os valores diferem do template e copie à mão qualquer mudança no schema:

```bash
git diff upstream/main -- src/site.config.ts
```

Depois faça o merge na `dev` e abra um pull request para a `main`. Quando a cópia está atualizada, `git log HEAD..upstream/main` não mostra nada e `git diff --stat upstream/main` lista só os arquivos pessoais.

## Licença

[MIT](./LICENSE)
