# 🌙 Midnight Breeze — VS Code Theme

**Midnight Breeze** é um tema escuro elegante para o Visual Studio Code, com uma paleta suave e contrastes equilibrados que reduzem o cansaço visual durante longas sessões de programação.

[![Build Status](https://github.com/leandroaps/midnight-breeze/workflows/Test%20Build/badge.svg)](https://github.com/leandroaps/midnight-breeze/actions)
[![VS Code Marketplace](https://img.shields.io/visual-studio-marketplace/v/leandroaps.vscode-theme-midnight-breeze)](https://marketplace.visualstudio.com/items?itemName=leandroaps.vscode-theme-midnight-breeze)
[![Downloads](https://img.shields.io/visual-studio-marketplace/d/leandroaps.vscode-theme-midnight-breeze)](https://marketplace.visualstudio.com/items?itemName=leandroaps.vscode-theme-midnight-breeze)

---

## ✨ Características

- Paleta escura suave com tons azulados e detalhes em amarelo/dourado
- Destaque claro para palavras-chave, funções e strings
- Estilo limpo, moderno e minimalista
- Ótimo para front-end, back-end, mobile ou qualquer stack

## 📦 Instalação

### Via VS Code Marketplace

1. Abra o VS Code
2. Vá para Extensions (Ctrl+Shift+X)
3. Procure por "Midnight Breeze"
4. Clique em Install

### Via Command Line

```bash
code --install-extension leandroaps.vscode-theme-midnight-breeze
```

## 🚀 Desenvolvimento

Este projeto usa GitHub Actions para automatizar o build e publicação:

- **Test Build**: Executa em cada push/PR para validar o tema
- **Publish**: Publica automaticamente no VS Code Marketplace quando uma tag é criada

### Scripts Disponíveis

```bash
# Construir o pacote VSIX
npm run build

# Publicar no marketplace (requer VSCE_PAT)
npm run publish
```

### Publicação Automática

Para publicar uma nova versão:

1. Atualize a versão no `package.json`
2. Commit as mudanças
3. Crie e push uma tag:

   ```bash
   git tag v1.0.3
   git push origin v1.0.3
   ```

O GitHub Action irá automaticamente:

- Construir o tema
- Publicar no VS Code Marketplace
- Criar um release no GitHub
- Fazer upload do arquivo VSIX

Para mais detalhes, veja [.github/SETUP.md](.github/SETUP.md)
