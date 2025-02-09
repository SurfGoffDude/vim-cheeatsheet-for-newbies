# Основы управления в Vim и Neovim

## Режимы в Vim
Vim работает в нескольких режимах, каждый из которых имеет свои особенности:

- **Normal mode (Режим по умолчанию)** — для перемещения по тексту, выполнения команд.
- **Insert mode (Режим вставки)** — для ввода текста.
- **Visual mode (Визуальный режим)** — для выделения текста.
- **Command-line mode (Режим командной строки)** — для ввода команд, таких как сохранение, выход и т.д.

### Переключение между режимами:
- **Normal mode → Insert mode**: Нажать `i`, `I`, `a`, `A`, `o`, `O` и т.д.
- **Insert mode → Normal mode**: Нажать `Esc`.
- **Normal mode → Visual mode**: Нажать `v` для выделения символов, `V` для выделения строк.
- **Normal mode → Command-line mode**: Нажать `:`.

## Основные команды

### Навигация:
- `h`, `j`, `k`, `l` — перемещение по символам (влево, вниз, вверх, вправо).
- `w` — перемещение на начало следующего слова.
- `b` — перемещение на начало предыдущего слова.
- `0` — перемещение в начало строки.
- `$` — перемещение в конец строки.
- `gg` — перемещение в начало файла.
- `G` — перемещение в конец файла.
- `Ctrl + f` — прокрутка страницы вниз.
- `Ctrl + b` — прокрутка страницы вверх.

### Редактирование:
- `x` — удалить символ.
- `dw` — удалить слово.
- `dd` — удалить строку.
- `d$` — удалить от курсора до конца строки.
- `yy` — копировать строку.
- `p` — вставить после курсора.
- `P` — вставить перед курсором.
- `u` — отменить последнее действие.
- `Ctrl + r` — повторить отмененное действие.

### Работа с файлами:
- `:w` — сохранить файл.
- `:q` — выйти из Vim.
- `:wq` — сохранить файл и выйти.
- `:q!` — выйти без сохранения изменений.
- `:e <filename>` — открыть файл.

### Поиск:
- `/pattern` — найти слово "pattern" в файле.
- `n` — найти следующее вхождение.
- `N` — найти предыдущее вхождение.

### Другие полезные команды:
- `:set number` — отображение номеров строк.
- `:set relativenumber` — отображение относительных номеров строк.
- `:set expandtab` — использовать пробелы вместо табуляции.
- `:set tabstop=4` — установить размер табуляции (по умолчанию 8).

## Копирование и вставка

В Vim нет прямой функции "копировать" и "вставить", как в других текстовых редакторах, но с помощью режима **Visual mode** и буферов обмена можно легко копировать и вставлять код:

### Копирование (выделение):
1. Перейдите в **Normal mode** (если вы не в нем, нажмите `Esc`).
2. Переместите курсор в начало текста, который хотите скопировать.
3. Нажмите `v` для выбора текста по символам или `V` для выделения целых строк.
4. Используйте движение курсора (например, `w`, `j`, `k`, `l`), чтобы выделить нужную часть текста.
5. После того как текст выделен, нажмите `y` для его копирования (запись в буфер).

### Вставка:
1. Перейдите в **Normal mode**.
2. Переместите курсор в место, куда хотите вставить текст.
3. Нажмите `p` для вставки после курсора или `P` для вставки перед курсором.

### Использование системного буфера обмена:
Если у вас настроен Vim с поддержкой системного буфера обмена (с опцией `+clipboard`), вы можете использовать команду для копирования в буфер обмена:

- `"+y` — копировать в системный буфер обмена (например, после выделения текста).
- `"+p` — вставить из системного буфера обмена.

Чтобы проверить, поддерживает ли ваш Vim буфер обмена, используйте команду `vim --version` и посмотрите на строку `+clipboard`. Если стоит `-clipboard`, то ваш Vim не поддерживает системный буфер обмена, и вам нужно будет перекомпилировать Vim с этой опцией или установить другой редактор.

## Установка плагинов
Вот полная конфигурация Vim для удобной работы с C++ и Python, включая установку необходимых плагинов. 

### **Установка менеджера плагинов**
Для начала вам нужно установить менеджер плагинов, например, [vim-plug](https://github.com/junegunn/vim-plug).

1. Установка `vim-plug`:
   ```bash
   curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
   ```

2. Создайте или откройте файл `~/.vimrc`:
   ```bash
   vim ~/.vimrc
   ```

---

### **Полная конфигурация `.vimrc`**

```vim
" === Основные настройки Vim ===
set nocompatible              " Отключение режима совместимости
filetype off                  " Отключение автозагрузки filetype для настройки плагинов

" === Настройка менеджера плагинов ===
call plug#begin('~/.vim/plugged')

" === Плагины ===
" Плагин для работы с файловой системой
Plug 'preservim/nerdtree'

" Поддержка синтаксиса и парсеров для Python и C++
Plug 'nvim-treesitter/nvim-treesitter', {'do': ':TSUpdate'}

" Автодополнение
Plug 'neoclide/coc.nvim', {'branch': 'release'}

" Подсветка синтаксиса и проверка PEP8 для Python
Plug 'vim-python/python-syntax'

" Поддержка LSP
Plug 'neovim/nvim-lspconfig'

" Поддержка автодополнения для C++
Plug 'hrsh7th/cmp-nvim-lsp'
Plug 'hrsh7th/nvim-cmp'

" Автоматические скобки
Plug 'jiangmiao/auto-pairs'

" Git интеграция
Plug 'tpope/vim-fugitive'

" Интерфейс для поиска файлов и текста
Plug 'nvim-telescope/telescope.nvim'

" Подсветка ошибок и форматирование
Plug 'dense-analysis/ale'

" Тема оформления
Plug 'gruvbox-community/gruvbox'

call plug#end()

" === Основные настройки ===
syntax on                    " Включить подсветку синтаксиса
filetype plugin indent on    " Включить плагины и настройки отступов
set number                   " Нумерация строк
set relativenumber           " Относительные номера строк
set expandtab                " Использовать пробелы вместо табуляции
set shiftwidth=4             " Размер отступа
set tabstop=4                " Табуляция равна 4 пробелам
set autoindent               " Автоматический отступ
set smartindent              " Умный отступ
set clipboard=unnamedplus    " Использовать системный буфер обмена
set background=dark          " Темная тема
colorscheme gruvbox          " Используем тему Gruvbox

" === Настройки для NERDTree ===
map <C-n> :NERDTreeToggle<CR>  " Переключение NERDTree с помощью Ctrl+N

" === Настройки для CoC (Completion) ===
" Установите поддержку Python и C++
autocmd BufEnter *.py,*.cpp,*.h,*.hpp call CocAction('activate')

" === Настройка ALE для проверки ошибок ===
let g:ale_linters = {
\   'python': ['flake8'],
\   'cpp': ['clangd']
\}
let g:ale_fixers = {
\   'python': ['black', 'isort'],
\   'cpp': ['clang-format']
\}
let g:ale_lint_on_save = 1
let g:ale_fix_on_save = 1

" === Настройки для Telescope ===
nnoremap <C-p> :Telescope find_files<CR>
nnoremap <C-f> :Telescope live_grep<CR>
```

---

### **Установка плагинов**
После добавления конфигурации в файл `.vimrc` выполните следующие шаги:

1. Откройте Vim:
   ```bash
   vim
   ```

2. Установите плагины:
   ```vim
   :PlugInstall
   ```

---

### **Установка дополнительных инструментов**

#### Для C++:
1. Установите `clangd` для работы LSP:
   ```bash
   sudo apt install clangd
   ```

2. Установите `clang-format` для форматирования кода:
   ```bash
   sudo apt install clang-format
   ```

#### Для Python:
1. Установите `flake8` для проверки PEP8:
   ```bash
   pip install flake8
   ```

2. Установите `black` для форматирования:
   ```bash
   pip install black
   ```

3. Установите `isort` для сортировки импортов:
   ```bash
   pip install isort
   ```

## **Установка и настройка Neovim**

---

### **1. Установка Neovim**

#### На macOS:
1. Установите Homebrew, если он еще не установлен:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. Установите Neovim через Homebrew:
   ```bash
   brew install neovim
   ```

3. Проверьте установку:
   ```bash
   nvim --version
   ```
   Вы должны увидеть версию Neovim.

#### На Ubuntu/Debian:
1. Обновите список пакетов:
   ```bash
   sudo apt update
   ```

2. Установите Neovim:
   ```bash
   sudo apt install neovim
   ```

3. Проверьте установку:
   ```bash
   nvim --version
   ```

#### На Windows:
1. Перейдите на официальный сайт Neovim: [https://neovim.io/](https://neovim.io/).
2. Скачайте установочный файл для Windows.
3. Установите его, следуя инструкциям.

---

### **2. Настройка Neovim**

#### Основной конфигурационный файл:
- Файл конфигурации для Neovim находится по пути:
  ```bash
  ~/.config/nvim/init.vim
  ```
  (или `~/.config/nvim/init.lua` для использования Lua).

1. Создайте директорию для конфигурации:
   ```bash
   mkdir -p ~/.config/nvim
   ```

2. Создайте файл конфигурации:
   ```bash
   touch ~/.config/nvim/init.vim
   ```

---

### **3. Установка менеджера плагинов**

#### Установка `vim-plug` для Neovim:
1. Выполните команду:
   ```bash
   curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
   ```

2. Проверьте, что `vim-plug` установлен, выполнив:
   ```bash
   ls ~/.local/share/nvim/site/autoload/
   ```

---

### **4. Пример конфигурации Neovim**

Добавьте следующие строки в файл `~/.config/nvim/init.vim`:

```vim
" === Основные настройки ===
set number                    " Включить нумерацию строк
set relativenumber            " Включить относительную нумерацию строк
set expandtab                 " Пробелы вместо табуляции
set tabstop=4                 " Длина табуляции
set shiftwidth=4              " Размер отступов
set smartindent               " Умный отступ
set clipboard=unnamedplus     " Использовать системный буфер обмена

" === Менеджер плагинов ===
call plug#begin('~/.config/nvim/plugged')

" Плагины
Plug 'preservim/nerdtree'          " Файловый менеджер
Plug 'nvim-treesitter/nvim-treesitter', {'do': ':TSUpdate'} " Подсветка синтаксиса
Plug 'neoclide/coc.nvim', {'branch': 'release'}  " Автодополнение и LSP
Plug 'tpope/vim-fugitive'          " Интеграция с Git
Plug 'junegunn/fzf', { 'do': './install --all' } " Быстрый поиск файлов
Plug 'junegunn/fzf.vim'            " Интеграция FZF
Plug 'gruvbox-community/gruvbox'   " Цветовая схема

call plug#end()

" === NERDTree настройки ===
map <C-n> :NERDTreeToggle<CR>      " Открыть/закрыть файловый менеджер

" === Цветовая схема ===
syntax enable
set background=dark
colorscheme gruvbox

" === Настройки CoC ===
autocmd BufEnter *.py,*.cpp,*.js call CocAction('activate')
```

---

### **5. Установка плагинов**

1. Откройте Neovim:
   ```bash
   nvim
   ```

2. Введите команду для установки всех плагинов:
   ```vim
   :PlugInstall
   ```

---

### **6. Установка дополнительных инструментов**

#### Для работы с LSP:
- Установите `clangd` для C++:
  ```bash
  brew install llvm  # для macOS
  sudo apt install clangd -y  # для Ubuntu/Debian
  ```

- Установите Python-пакеты:
  ```bash
  pip install flake8 black isort
  ```

#### Для поиска файлов:
- Убедитесь, что у вас установлен `fzf`:
  ```bash
  brew install fzf  # для macOS
  sudo apt install fzf -y  # для Ubuntu/Debian
  ```

---

### **7. Проверка работы Neovim**

1. Создайте файл для теста, например:
   ```bash
   touch test.py
   ```

2. Откройте его в Neovim:
   ```bash
   nvim test.py
   ```

3. Проверьте:
   - Подсветку синтаксиса.
   - Работу автодополнения (например, CoC).
   - Работу файлового менеджера `NERDTree` с помощью `Ctrl + n`.

