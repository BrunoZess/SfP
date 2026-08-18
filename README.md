# 🎮 Promoções de Jogos

Site estático que mostra jogos em promoção, gerado automaticamente com Python
a partir da [API pública da CheapShark](https://apidocs.cheapshark.com/).

## Como funciona

1. `fetch_deals.py` busca os dados de preços na API da CheapShark.
2. O script gera um `index.html` com os jogos, preço antigo, preço novo e desconto.
3. O GitHub Actions (`.github/workflows/update.yml`) roda esse script
   automaticamente todo dia e faz commit do `index.html` atualizado.
4. O GitHub Pages publica esse `index.html` como um site.

## Rodando localmente

```bash
pip install -r requirements.txt
python fetch_deals.py
# abra o index.html gerado no navegador
```

## Publicando no GitHub Pages

1. Crie um repositório novo no GitHub e suba estes arquivos:
   ```bash
   git init
   git add .
   git commit -m "primeiro commit"
   git branch -M main
   git remote add origin https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
   git push -u origin main
   ```
2. No repositório, vá em **Settings > Pages**.
3. Em "Build and deployment", escolha **Deploy from a branch**.
4. Selecione a branch `main` e a pasta `/ (root)`.
5. Salve. Em alguns minutos seu site estará em:
   `https://SEU-USUARIO.github.io/SEU-REPOSITORIO/`

## Automatização

O workflow em `.github/workflows/update.yml` já está configurado para rodar
todo dia às 06:00 (horário de Brasília) e atualizar o `index.html` sozinho,
fazendo commit automático. Você também pode rodá-lo manualmente na aba
**Actions** do repositório, clicando em "Run workflow".

> Importante: em **Settings > Actions > General > Workflow permissions**,
> marque a opção "Read and write permissions" para o Actions poder commitar
> as atualizações.

## Customizando

No arquivo `fetch_deals.py`, o dicionário `PARAMS` controla a busca:

- `storeID`: qual loja (1 = Steam, 25 = Epic Games, 7 = GOG, etc — lista completa em
  `https://www.cheapshark.com/api/1.0/stores`)
- `upperPrice`: preço máximo em dólar
- `pageSize`: quantos jogos mostrar
- `sortBy`: critério de ordenação (`Savings`, `Price`, `Title`, etc)
