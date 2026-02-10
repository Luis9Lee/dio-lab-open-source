{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "printWidth": 80,
  "trailingComma": "es5"
}

{
  "name": "automacao-dio-lab",
  "version": "1.0.0",
  "description": "Configuração de automação de formatação",
  "scripts": {
    "format": "prettier --write .",
    "check-format": "prettier --check ."
  },
  "devDependencies": {
    "prettier": "^3.0.0"
  }
}

name: Verificação de Formatação

# Dispara a automação quando houver push ou pull request na branch main/master
on:
  push:
    branches: [ "main", "master" ]
  pull_request:
    branches: [ "main", "master" ]

jobs:
  check-formatting:
    runs-on: ubuntu-latest

    steps:
      # 1. Baixa o código do repositório
      - name: Checkout do código
        uses: actions/checkout@v4

      # 2. Instala o Node.js (necessário para rodar o Prettier)
      - name: Instalar Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      # 3. Instala as dependências listadas no package.json
      - name: Instalar dependências
        run: npm install

      # 4. Roda o comando de verificação
      - name: Verificar formatação (Prettier)
        run: npm run check-format
