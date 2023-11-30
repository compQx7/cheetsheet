# 調査
| 内容 | key |
| --- | --- |
| 定義移動 | F12 |
| 定義表示 | Alt + F12 |
| 参照表示 | Shift + F12 |
| ホバー情報表示 | gh |

## フォーカス移動
| 内容 | key |
| --- | --- |
| サイドバー | Ctrl + 0 |
| エディタグループN | Ctrl + [1-8] |
| ターミナル | Ctrl + @ |

## パネル
Ctrl + b: サイドバー 表示・非表示
Ctrl + Shift + e: エクスプローラーへ移動

## search
| 内容 | key |
| --- | --- |
| 全検索 | Ctrl + Shift + f |
| 全検索 次・前に移動 | F4、Shift + F4 |
| 全検索 履歴表示 |  入力フィールド内で Alt + ↑↓ |
| シンボル名検索（アウトライン表示） | Ctrl + Shift + o<br />Ctrl + Shift + o: |
| ファイル名検索(quick open) | Ctrl + p |

# Edit
F12: 定義へ移動
Alt + [<-,->]: 遷移前へ移動、遷移後へ移動
Ctrl + Space: インテリセンス（入力補完）

| キーワードを含む行を削除 |
Ctrl f で検索
Alt Enter で全選択
Ctrl Shift k で行削除

| キーワードを文字やタグで囲む |
選択範囲上で Shift + ["'(){}[]<>]

| コードフォーマット 整形（JSON整形も可能） | Shift + Alt + f |

| マルチカーソル | Alt + Ctrl + ↑↓<br />Alt + クリック |

## 全体
Ctrl + Shift + p: 便利コマンド
Ctrl + .: コードアクション？

Ctrl + k, Ctrl + s: ショートカット一覧

F11: 全画面表示切替

# favorite settings
定期的にショートカットやコマンド、設定ファイル、プラグインを調べると良い。

## extentions
vim
Github Copilot

## ショートカット変更
| Focus on outline view | Alt + o

## vim拡張
[vim.md](./vim.md)

Ctrl + c: vimのインサートモードからコマンドモードへ

| 定義へ移動 |
gd
| 選択範囲拡大 |
(VisualMode)af
| カーソル位置の単語選択（複数回押すとマルチカーソル） |
gb
| Visualモードで行末まで選択 |
g_
| Visualモードでサラウンド |
S["'[](){}]
ds["'[](){}]
ys[motion]["'[](){}]
cs["'[](){}]["'[](){}]

### エクスプローラー
| 内容 | key |
| --- | --- |
| 上下移動 | k, j |
| 上下に大きく移動 | Ctrl + u、Ctrl + d |
| 最上、最下 | gg, G |
| ツリー展開 | o, h, l |
| エクスプローラーにいるまま開く | o, Space |
| 開いてエディタへ移動 | l |
| 検索。検索後はヒットしたもののみで移動可能(j,k)。<br />展開されていないフォルダは対象外。 | Ctrl + f |
| 検索。gから始まる場合など挙動がおかしい。 | / |

## 設定ファイル
1. VSCode上でDeveloper Toolsを開く
1. Inspect Context Key で調べる領域をクリック
1. Developer Toolsのコンソールにプロパティが表示されるので検索して良しなに活用する

settings.json
```json
{
    "workbench.tree.indent": 15,
    "editor.wordWrap": "on",
    "editor.minimap.enabled": false,

    // vim設定
    // "vim.vimrc.enable": true,
    // "vim.vimrc.path": "~/.vimrc",
    "vim.hlsearch": true,
    "vim.useSystemClipboard": true, // クリップボードを使う
    "vim.sneak": true,
    "vim.foldfix": true, // 折りたたみを修正
    "vim.enableNeovim": true, // neovimを有効化
    "vim.leader": "<space>", // leaderキーを設定
    "vim.easymotion": true,
    "vim.insertModeKeyBindingsNonRecursive": [
        { "before": [ "j", "f" ], "after": [ "<Esc>" ] },
    ],
    "vim.normalModeKeyBindingsNonRecursive": [
        { "before": [ "<C-p>" ], "commands": [ "workbench.action.quickOpen" ] },
        // 移動補助
        { "before": ["K"], "after": ["5", "k"] },
        { "before": ["J"], "after": ["5", "j"] },
        { "before": [ "<C-k>" ], "after": [ "7", "k", "z", "z" ] },
        { "before": [ "<C-j>" ], "after": [ "7", "j", "z", "z" ] },
        { "before": [ "<C-y>" ], "after": [ "5", "<C-y>" ] },
        { "before": [ "<C-e>" ], "after": [ "5", "<C-e>" ] },
        { "before": [ "<leader>", "h" ], "after": [ "^" ] },
        { "before": [ "<leader>", "l" ], "after": [ "$" ] },
        { "before": [ "<leader>", "m" ], "after": [ "%" ] },
        // 検索対象を画面中央に表示
        { "before": [ "n" ], "after": [ "n", "z", "z" ] },
        { "before": [ "N" ], "after": [ "N", "z", "z" ] },
        { "before": [ "*" ], "after": [ "*", "z", "z" ] },
        { "before": [ "#" ], "after": [ "#", "z", "z" ] },
        // カーソル位置の単語をマルチカーソルで選択
        { "before": [ "<C-n>" ], "after": [ "g", "b" ] },
        // ハイライト除去
        { "before": [ "<leader>", "\/" ], "commands": [ ":noh" ] },
        // ワークスペース内シンボル検索
        { "before": [ "<leader>", "t" ], "commands": [ "workbench.action.showAllSymbols" ] },
        // 変数の参照箇所の表示
        { "before": [ "g", "f" ], "commands": [ "editor.action.referenceSearch.trigger" ] },
        // 左タブへ移動
        { "before": ["C-h"], "commands": [ "workbench.action.previousEditor" ] },
        // 右タブへ移動
        { "before": ["C-l"], "commands": [ "workbench.action.nextEditor" ] },
        // タブを左に移動
        { "before": ["<leader>", "<"], "commands": [ ":tabm -1" ] },
        // タブを右に移動
        { "before": ["<leader>", ">"], "commands": [ ":tabm +1" ] },
    ],
    "vim.visualModeKeyBindingsNonRecursive": [
        // 移動補助
        { "before": ["K"], "after": ["5", "k"] },
        { "before": ["J"], "after": ["5", "j"] },
        { "before": [ "<leader>", "h" ], "after": [ "^" ] },
        { "before": [ "<leader>", "l" ], "after": [ "$" ] },
        { "before": [ "<leader>", "m" ], "after": [ "%" ] },
        // カーソル位置の単語をマルチカーソルで選択
        { "before": [ "<C-n>" ], "after": [ "g", "b" ] },
    ],
}
```

keybindings.json
```json
[
    // ########################################
    // フォーカス
    // ########################################
    // エディターフォーカス
    {
        "key": "ctrl+e",
        "command": "workbench.action.focusActiveEditorGroup",
        "when": "!editorTextFocus"
    },
    // アウトラインフォーカス
    {
        "key": "alt+o",
        "command": "outline.focus",
        "when": "focusedView == workbench.explorer.fileView || editorTextFocus"
    },
    // ########################################
    // サイドバー操作
    // ########################################
    {
        "key": "shift+j",
        "command": "runCommands",
        "args": {
            "commands": ["list.focusDown", "list.focusDown", "list.focusDown", "list.focusDown", "list.focusDown"]
        },
        "when": "!inputFocus && (focusedView == workbench.explorer.fileView || focusedView == outline || focusedView == workbench.view.search)"
    },
    {
        "key": "shift+k",
        "command": "runCommands",
        "args": {
            "commands": ["list.focusUp", "list.focusUp", "list.focusUp", "list.focusUp", "list.focusUp"]
        },
        "when": "!inputFocus && (focusedView == workbench.explorer.fileView || focusedView == outline || focusedView == workbench.view.search)"
    },
    {
        "key": "shift+o",
        "command": "list.collapseAll",
        "when": "!inputFocus && (focusedView == workbench.explorer.fileView || (focusedView == outline && !outlineAllCollapsed) || (focusedView == workbench.view.search && treeElementCanCollapse))"
    },
    {
        "key": "shift+o",
        "command": "search.action.expandSearchResults",
        "when": "!inputFocus && focusedView == workbench.view.search && !treeElementCanCollapse"
    },
    {
        "key": "shift+o",
        "command": "outline.expand",
        "when": "!inputFocus && focusedView == outline && outlineAllCollapsed"
    },
    {
        "key": "ctrl+[",
        "command": "search.focus.nextInputBox",
        "when": "focusedView == workbench.view.search && searchViewletVisible"
    },
    // ########################################
    // コマンドパレット
    // ########################################
    // コマンドパレットや補完の上下移動
    {
        // "key": "ctrl+j",
        "key": "ctrl+n",
        "command": "selectNextSuggestion",
        "when": "suggestWidgetMultipleSuggestions && suggestWidgetVisible && textInputFocus"
    },
    {
        // "key": "ctrl+k",
        "key": "ctrl+p",
        "command": "selectPrevSuggestion",
        "when": "suggestWidgetMultipleSuggestions && suggestWidgetVisible && textInputFocus"
    },
    {
        // "key": "ctrl+j",
        "key": "ctrl+n",
        "command": "workbench.action.quickOpenSelectNext",
        "when": "inQuickOpen",
    },
    {
        // "key": "ctrl+k",
        "key": "ctrl+p",
        "command": "workbench.action.quickOpenSelectPrevious",
        "when": "inQuickOpen ",
    },
    // コマンドパレットや補完を閉じる
    {
        "key": "ctrl+[",
        "command": "workbench.action.closeQuickOpen",
        "when": "inQuickOpen"
    },
]
```