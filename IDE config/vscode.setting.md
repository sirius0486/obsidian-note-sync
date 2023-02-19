> [!info] > 参考自 一个托尼(antfu)的 vscode 配置

## Link
https://github.com/antfu/vscode-settings

```md
Anthony's VS Code Settings

.vscode/settings.json
.vscode/extensions.json
.vscode/global.code-snippets
```


## setting

### .vscode/settings.json
```json
{
  "workbench.iconTheme": "file-icons",
  "workbench.colorTheme": "Vitesse Light",
  "editor.fontSize": 13,
  "editor.fontFamily": "JetBrains Mono",
  "editor.fontLigatures": true,
  "editor.wordWrap": "on",
  "editor.formatOnSave": true,
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "editor.tokenColorCustomizations": {
    "comments": "#1fd160"
  },
  "terminal.integrated.fontFamily": "MesloLGM NF",
  "explorer.confirmDelete": false,
  "git.suggestSmartCommit": false,
  "typescript.updateImportsOnFileMove.enabled": "always",
  "reactSnippets.settings.prettierEnabled": true,
  "unocss.root": ["packages/client"]
}


```

### .vscode/extensions.json


### .vscode/global.code-snippets



## plugins

### git
- git lens
- git graph
- git history


### snippets
- volar 
- ES7+ React/Redux/React-Native snippets
- UnoCSS

### preview
- Svg Preview
- Image Preview
- MDX

### debug
- Import Cost
- Error Lens

### beauty

- file icons / vscode icons
- vitesse theme / atom theme
- Jetbrain Mono / Input Mono




## 备忘录
- markdown 打开自动预览
- 自动换行
- 连体字开启
- 绿色注释
- 自动格式化