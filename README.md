# vim-run-python
> Vim plugin to run Python code inside Vim, without using a terminal. With a single keypress, the output from your current Python file will be placed in a new buffer (window) at the bottom of your editor.

- **Intelligent Environment Finding:** When you press your key binding, it searches your current directory, and several parent directories, to find a python virtual environment named env. If none are found, then your machine's global python kernel will be used.
- Current script gets executed silently, and its output is placed into a new Vim buffer at the bottom of your window.
- This new buffer is dynamically sized, so it's only tall enough to fit the output of your script. Its height is updated every time you execute.

**IMPORTANT**

> This is designed to work with GVIM on Mac/Unix systems only. However, the code can easily be modified to work with Windows. See below for an explanation:

<details>
<summary><i>How to modify code for Windows</i></summary>

- Find the source code in your vim files, in your plugin manager's respective directory. For example, if using Plug, go to `plugged/vim-run-python/plugin/run-python.vim`.
- Near the middle of the file, find the block of code that starts with:
- ```vim
if filereadable("env/pyvenv.cfg") == 1
    silent exe ".!source env/bin/activate&&python3 " . shellescape(s:current_buffer_file_path, 2)
...
```
- Modify all the file paths in double quotes to match Windows format. All forward-slashes must be replaced with backslashes. Also, the command to activate a Python *venv* is different for windows: Replace all instances of `env/bin/activate` with `env/Scripts/activate`. If using *virtualenv* or another type of environment, see its documentation for help.

</details>

> By default, this plugin assumes all your python virtual environments are named `/env`. If using a different naming convention, use the Windows instructions above to find the block of code that activates the environment, and replace all instances of `env` as needed.

## INSTALLATION
1. If using Plug as your plugin manager, paste into the plugin section of your ```vimrc```:
```vim
Plug 'ryayoung/vim-run-python'
```
2. Run **```:PlugInstall```** after saving and re-opening Vim.

## HOW TO USE

In your `vimrc`, declare a key mapping to execute `:call ExecutePythonNewBuffer()<CR>`. I like to use `<leader>r`. For example...

```vim
" In your vimrc...
nnoremap <Leader>r :call ExecutePythonNewBuffer()<CR>
```

## CUSTOMIZATION

This is a simple plugin. Only about 90 lines in total - half of which are settings. If you've come this far, I recommend reading through the source code and making adjustments or customizations as desired. To find the source code, navigate to your vim files, and find the directory for your plugin manager. (If using Plug, go to `/plugged`). Then, find `vim-run-python/plugin/run-python.vim`.
