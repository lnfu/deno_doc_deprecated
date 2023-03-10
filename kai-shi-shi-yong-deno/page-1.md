# 設置您的環境

Deno CLI 包含許多開發應用常用的工具，包括一個完整的語言伺服器，加強您選用的 IDE。您只需要[安裝](https://deno.land/manual@v1.30.3/getting\_started/installation)，即可使用這些[工具](https://deno.land/manual@v1.30.3/getting\_started/command\_line\_interface)。

## **使用編輯器／IDE**

編輯器／IDE 廣泛支援使用 Deno。接下來的部分，將提供有關如何在編輯器使用 Deno 的資訊。多數編輯器透過語言伺服器協定與 Deno CLI 集成語言伺服器，直接與 Deno 整合。

如果您嘗試編寫或協助社群整合至 Deno 語言伺服器，Deno CLI 程式 repo 中存有一些[說明文檔](https://github.com/denoland/deno/tree/main/cli/lsp#deno-language-server)。您也可以自由地加入 [Discord 社群](https://discord.gg/deno)的 `#dev-lsp` 頻道。

### Visual Studio Code

這裡有個名為[vscode\_deno](https://marketplace.visualstudio.com/items?itemName=denoland.vscode-deno) 的 [Visual Studio Code](https://code.visualstudio.com/) 官方擴充。安裝後，它將會連接至 Deno CLI 內建的語言伺服器。

由於多數人在混合環境中工作，該擴充預設不會如同啟動 Deno 一般啟動工作區，並且需要 `"deno.enable"` 參數被設置。您可以自行改變設定，或者透過指令面版 `Deno: Initialize Workspace Configuration` 以起始您的專案。

更多資訊可以在手冊 [Using Visual Studio Code](https://deno.land/manual@v1.30.3/references/vscode\_deno) 文中找到。

### **JetBrains IDEs**

您可以在 WebStorm 與其他 [JetBrains IDEs](https://www.jetbrains.com/products/#type=ide)（包括 PhpStorm、IntelliJ IDEA Ultimate 和 PyCharm Professional）中得到使用 Deno 的協助。為此，請從 _Preferences / Settings | Plugins - Marketplace_ 安裝 [Deno 官方插件](https://plugins.jetbrains.com/plugin/14382-deno)。

查看這篇[部落格文章（英文）](https://blog.jetbrains.com/webstorm/2020/06/deno-support-in-jetbrains-ides/)，了解如何開始使用 Deno。

### **Vim/Neovim（使用插件）**

透過 [coc.nvim](https://github.com/neoclide/coc.nvim)、[vim-easycomplete](https://github.com/jayli/vim-easycomplete) 與 [ALE](https://github.com/dense-analysis/ale)，Deno 能在 [Vim](https://www.vim.org/) 與 [Neovim](https://neovim.io/) 上使用。coc.nvim 提供與 Deno 語言伺服器整合的插件，ALE 則使其能_隨開即用_。

### **Neovim 0.6+（使用內建語言伺服器）**

使用 Deno 語言伺服器，請安裝 [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig/) 並依照指引啟用[支援的 Deno 設置](https://github.com/neovim/nvim-lspconfig/blob/master/doc/server\_configurations.md#denols)。

請注意，如果您也有 `tsserver` 作為 LSP 客戶端，你可能會遇到 `tsserver` 與 `denols` 都接到您現有緩衝的問題。解決這個問題，請確保在 `tsserver` 與 `denols` 中，設置不同的 `root_dir`。您可能還需要設置 `tsserver` 的 `single_file_support` 為 `false`，以避免其以 `single file mode` 執行。以下是一個設置範例：

```vim
nvim_lsp.denols.setup {
  on_attach = on_attach,
  root_dir = nvim_lsp.util.root_pattern("deno.json", "deno.jsonc"),
}

nvim_lsp.tsserver.setup {
  on_attach = on_attach,
  root_dir = nvim_lsp.util.root_pattern("package.json"),
  single_file_support = false
}
```

對 Deno 而言，上面的範例假設專案的根目錄存在一個 `deno.json` 或 `deno.jsonc` 檔案。

#### **coc.nvim**

一旦您安裝 [coc.nvim](https://github.com/neoclide/coc.nvim/wiki/Install-coc.nvim)，您需要透過 `:CocInstall coc-deno` 安裝所需的 [coc-deno](https://github.com/fannheyward/coc-deno)。

一旦插件完成安裝，並且您想要在工作區啟用 Deno，請執行 `:CocCommand deno.initializeWorkspace` 指令，您應該就能使用指令如 `gd` （移至定義）與 `gr` （移至／尋找參考）。

#### ALE

ALE 透過 Deno 語言伺服器_隨開即用地_支援 Deno，並且在多數使用情境不需要額外的配置。[安裝 ALE](https://github.com/dense-analysis/ale#installation) 後，您可以執行指令 [`:help ale-typescript-deno`](https://github.com/dense-analysis/ale/blob/master/doc/ale-typescript.txt) 來取得有關可用配置選項的資訊。

有關如何設定 ALE （例如按鍵綁定）的資訊，請參考[官方文檔](https://github.com/dense-analysis/ale#usage)。

#### **Vim-EasyComplete**

Vim-EasyComplete 不須其他配置即可支援 Deno。一但您完成[安裝 vim-easycomplete](https://github.com/jayli/vim-easycomplete#installation) 且未安裝 deno，您需要透過`:InstallLspServer deno` 安裝。您可以從[官方文檔](https://github.com/jayli/vim-easycomplete)中獲得更多資訊。\


### **Emacs**

**lsp 模式**

Emacs 透過 Deno 語言伺服器，以 [lsp 模式](https://emacs-lsp.github.io/lsp-mode/)支援 Deno。一旦 [lsp 模式安裝](https://emacs-lsp.github.io/lsp-mode/page/installation/)完成，它應能支援 Deno，也可透過[配置](https://emacs-lsp.github.io/lsp-mode/page/lsp-deno/)以支援各式設定。

#### eglot

您也可以透過 [`eglot`](https://github.com/joaotavora/eglot) 使用 Deno 內建的語言伺服器。

這是一個以 eglot 使用 Deno 的配置範例：

```
(add-to-list 'eglot-server-programs '((js-mode typescript-mode) . (eglot-deno "deno" "lsp")))

  (defclass eglot-deno (eglot-lsp-server) ()
    :documentation "A custom class for deno lsp.")

  (cl-defmethod eglot-initialization-options ((server eglot-deno))
    "Passes through required deno initialization options"
    (list :enable t
    :lint t))
```

### Atom

[Pulsar 編輯器（原名 Atom）](https://pulsar-edit.dev/)支援透過 [atom-ide-deno](https://web.pulsar-edit.dev/packages/atom-ide-deno) 套件包支援 Deno 語言伺服器集成。`atom-ide-deno` 需要 Deno 命令列介面與 [atom-ide-base](https://web.pulsar-edit.dev/packages/atom-ide-base) 套件包被安裝完成。

### **Sublime Text**

[Sublime Text](https://www.sublimetext.com/) 支援透過 [LSP 套件包](https://packagecontrol.io/packages/LSP)連接至 Deno 語言伺服器。您可能也想安裝 [TypeScript 套件包](https://packagecontrol.io/packages/TypeScript)以獲得完整的語法高亮。

一旦您完成 LSP 套件包安裝，您會想要增加配置到 `.sublime-project` 配置，如下：

```
{
  "settings": {
    "LSP": {
      "deno": {
        "command": ["deno", "lsp"],
        "initializationOptions": {
          // "config": "", // Sets the path for the config file in your project
          "enable": true,
          // "importMap": "", // Sets the path for the import-map in your project
          "lint": true,
          "unstable": false
        },
        "enabled": true,
        "languages": [
          {
            "languageId": "javascript",
            "scopes": ["source.js"],
            "syntaxes": [
              "Packages/Babel/JavaScript (Babel).sublime-syntax",
              "Packages/JavaScript/JavaScript.sublime-syntax"
            ]
          },
          {
            "languageId": "javascriptreact",
            "scopes": ["source.jsx"],
            "syntaxes": [
              "Packages/Babel/JavaScript (Babel).sublime-syntax",
              "Packages/JavaScript/JavaScript.sublime-syntax"
            ]
          },
          {
            "languageId": "typescript",
            "scopes": ["source.ts"],
            "syntaxes": [
              "Packages/TypeScript-TmLanguage/TypeScript.tmLanguage",
              "Packages/TypeScript Syntax/TypeScript.tmLanguage"
            ]
          },
          {
            "languageId": "typescriptreact",
            "scopes": ["source.tsx"],
            "syntaxes": [
              "Packages/TypeScript-TmLanguage/TypeScriptReact.tmLanguage",
              "Packages/TypeScript Syntax/TypeScriptReact.tmLanguage"
            ]
          }
        ]
      }
    }
  }
}
```

### Nova

[Nova 編輯器](https://nova.app/)可透過 [Deno 擴充](https://extensions.panic.com/extensions/jaydenseric/jaydenseric.deno)整合 Deno 語言伺服器。

### **GitHub Codespaces**

[GitHub Codespaces](https://github.com/features/codespaces) 使您能夠在線上或遠端地在您的本地電腦中開發，不需要配置或安裝 Deno。它目前為搶先體驗。

若一個專案是啟用 Deno 的專案且 repo 中包含 `.devcontainer` 配置，在 GitHub Codespaces 中開啟專案應該能正常運作。如果您開始一項新專案。或您想要將 Deno 加入現存的程式碼空間，可以透過指令面板選擇 `Codespaces: Add Development Container Configuration Files...`，並選擇 `Show All Definitions...`，再搜尋 `Deno` 定義。

完成設定後，您需要重新建置您的容器，使 Deno 命令列介面被加入容器裡。重新建置後，該程式碼空間將支援 Deno。

### **Kakoune**

Kakoune 支援透過 kak-lsp 客戶端連接至 Deno 語言伺服器。一旦 kak-lsp 安裝完成，一個使它連接 Deno 語言伺服器的配置範例，是將以下加入您的 kak-lsp.toml：

```
[language.typescript]
filetypes = ["typescript", "javascript"]
roots = [".git"]
command = "deno"
args = ["lsp"]
[language.typescript.settings.deno]
enable = true
lint = true
```

## **Shell completions**

Deno 命令列介面支援生成 shell completion 資訊給命令列。透過使用 `demo completions <shell>`，Deno 命令列介面會將補全輸出至標準輸出。目前支援的 shells 有：

* bash
* elvish
* fish
* powershell
* zsh

### bash 範例

輸出補全並將它們加入環境中：

```
> deno completions bash > /usr/local/etc/bash_completion.d/deno.bash
> source /usr/local/etc/bash_completion.d/deno.bash
```
