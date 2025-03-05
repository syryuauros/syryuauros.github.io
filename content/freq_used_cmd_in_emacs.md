# freq-used-cmd

## Display
| Command                                | Description                                          |
|----------------------------------------|------------------------------------------------------|
| opacity control in emacs               | M-x doom/set-frame-opacity                          |
| windows opacity control                | picom -cf -i 0.8 --use-ewmh-active-win &            |
| show hide folder in dired              | S-h                                                  |
| command history                        | C-r                                                  |
| screen saver, auto-display-off         | $ xset s off -dpms                                  |
| screen saver on                        | $ xset s on                                         |
| screen saver time set                  | $ xset s 600                                        |

## edit (vim, emacs, sed)

**sed REFs** [출처: https://engineer-mole.tistory.com/235]
| Command                                 | Description                                          |
|-----------------------------------------|------------------------------------------------------|
| how to edit vim in emacs                | insert mode is same, when you want to save and out from vim |
|                                         | 'Esc' -> 'C-c C-c' -> 'i' -> ':wq'                   |
| vim as a default editor                 | $ export EDITOR=/run/current-system/sw/bin/vim       |
| find & change                           | :%s/[word-to-find]/[word-target-for-changed]         |
|                                         | :%s/[word-to-find]/[word-target-for-changed]/c       |
|                                         | select range -> :`<,`>s/[word-to-find]/[word-target-for-changed] |
|                                         | C-v (vertical range)                                |
|                                         | C-v -> S-i -> [string-to-replace] -> ESC            |
| find selected word                      | select range -> '*' or '#'                           |
|                                         | '*' for forward, '#' for backward                   |
| auto-completion                         | C-p                                                  |
| key binding                             | M-x describe key                                     |
|                                         | M-x global set key, global unset key                 |
|                                         | (if key binding is already exist then documentation appears) |
|                                         | M-x +lookup/(definition, reference, file)           |
| move to scope                           |                                                      |
| prev/next buffer                        | M-x previous-buffer, next-buffer                     |
| auto-align                              | select range -> '='                                  |
| Emacs menu                              | F10                                                  |
| marking                                 | C-spc                                                |
| cursor jump back to marked position     | g-;                                                  |
| cursor jump to line                     | M-g g, (add to config.el, M-s M-s)                   |

## searching & navigating
- [search-project-for-symbol-at-point](https://chat.openai.com/c/6f494164-3e37-4c7d-bab3-37fab38736e0)
- [Emacs Grep Find](http://xahlee.info/emacs/emacs/emacs_grep_find.html)

| Command                                    | Description                                          |
|--------------------------------------------|------------------------------------------------------|
| search-project-for-symbol-at-point        | M-*                                                  |
| rg                                         | M-x rg (add to config.el, M-s M-d)                   |
|                                           | $ rg "pattern" /path/to/directory                   |
| lgrep                                      | M-x lgrep                                            |

## edit| process kill
| Command                                  | Description                                           |
|------------------------------------------|-------------------------------------------------------|
| Process kill                             | $ pkill [process name] or $ kill -9 [process number]   |
| vim tutorial                             | $ vimtutor                                           |

## system
| Command                                   | Description                                             |
|-------------------------------------------|---------------------------------------------------------|
| nixos rebuild                            | $ sudo nixos-rebuild switch --flake .#syryuhds --impure  |
| nixos home-manager                       | $ home-manager switch --flake .#auros --impure          |

## nix & nix flake
| Command                                   | Description                                             |
|-------------------------------------------|---------------------------------------------------------|
| nix repl                                  | $ nix repl                                              |
| nix repl help                             | nix-repl> :help                                         |
| load pkgs                                 | nix-repl> pkgs = import <nixpkgs> {}                    |
| load flake                                | nix-repl> :lf .                                         |
| find function in pkgs                    | nix-repl> pkgs.writeT [Tab] -> makes pkgs.writeText     |
| find builtin function                    | nix-repl> :doc builtins.isP [Tab] -> makes builtins.isPath |

**How to set pwd as a specific folder**
```bash
script = ''
  cd /home/hproxy/secrets
  ls -lah
  ${pkgs.su}/bin/su - hproxy -c "${inputs.agenix.packages.x86_64-linux.default}/bin/agenix -d /home/hproxy/secrets/wg-hproxy.age | ${pkgs.sudo}/bin/sudo ${pkgs.coreutils}/bin/tee /run/agenix.d/1/wg"
 '';
