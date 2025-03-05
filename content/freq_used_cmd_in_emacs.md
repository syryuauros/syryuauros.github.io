#+title: freq-used-cmd

* Display
| opacity control in emacs       | :: | M-x doom/set-frame-opacity               |   |
| windows opacity control        | :: | picom -cf -i 0.8 --use-ewmh-active-win & |   |
| show hide folder in dired      | :: | S-h                                      |   |
| command history                | :: | C-r                                      |   |
| screen saver, auto-display-off | :: | $ xset s off -dpms                       |   |
| screen saver on                | :: | $ xset s on                              |   |
| screen saver time set          | :: | $ xset s 600                             |   |

* edit (vim, emacs, sed)
**  sed REFs  출처: https://engineer-mole.tistory.com/235 [매일 꾸준히, 더 깊이:티스토리]
| how to edit vim in emacs            | :: | insert mode is same, when you want to save and out from vim      |                                           |
|                                     | :: | 'Esc' -> 'C-c C-c' -> 'i' -> ':wq'                               |                                           |
| vim as a default editor             |    | $ export EDITOR=/run/current-system/sw/bin/vim                   |                                           |
| find & change                       | :: | :%s/[word-to-find]/[word-target-for-changed]                     |                                           |
|                                     | :: | :%s/[word-to-find]/[word-target-for-changed]/c                   | for checking                              |
|                                     | :: | select range -> :`<,`>s/[word-to-find]/[word-target-for-changed] | for a range                               |
|                                     | :: | C-v                                                              | vertical range                            |
|                                     |    | C-v -> S-i -> [string-to-replace] -> ESC                         |                                           |
| find selected word                  |    | select range -> '*' or '#'                                       | '*' for forward, '#' for backward         |
| auto-completion                     | :: | C-p                                                              |                                           |
|                                     |    |                                                                  |                                           |
| key binding                         | :: | M-x describe key                                                 | confirm key                               |
|                                     | :: | M-x global set key, global unset key                             | set key binding                           |
|                                     |    | (if key binding is already exist then documentation appears)     | M-x +lookup/(definition, reference, file) |
|                                     |    | (pre-fix like C-r or M-r must needed)                            |                                           |
| move to scope                       | :: |                                                                  |                                           |
| prev/next buffer                    | :: | M-x previous-buffer, next-buffer                                 |                                           |
|                                     |    |                                                                  |                                           |
| auto-allign                         | :: | select range -> '='                                              |                                           |
| Emacs menu                          | :: | F10                                                              |                                           |
|                                     |    |                                                                  |                                           |
| marking                             | :: | C-spc                                                            | set-mark-command                          |
| cursor jump back to marked position | :: | g-;                                                              | evil-go-to-last-change                    |
| cursor jump to line                 | :: | M-g g,  (add to config.el, M-s M-s)                              | goto-line                                 |

* searching & navigating
+ https://chat.openai.com/c/6f494164-3e37-4c7d-bab3-37fab38736e0
+ http://xahlee.info/emacs/emacs/emacs_grep_find.html
| search-project-for-symbol-at-point | :: | M-*                                |
| rg                                 | :: | M-x rg (add to config.el, M-s M-d) |
|                                    |    | $ rg "pattern" /path/to/directory  |
| lgrep                              | :: | M-x lgrep                          |

* edit| process kill | :: | $ pkill [process name]  or $ kill -9 [process number] |
| vim tutorial | :: | $ vimtutor |
|              |    |            |
* system
| nixos rebuild      | :: | $ sudo nixos-rebuild switch --flake .#syryuhds --impure |
| nixos home-manager | :: | $ home-manager switch --flake .#auros --impure          |
|                    |    |                                                         |
|                    |    |                                                         |

* nix & nix flake
| nix repl              | :: | $ nix repl                                                 |
| nix repl help         | :: | nix-repl> :help                                            |
| load pkgs             | :: | nix-repl> pkgs = import <nixpkgs> {}                       |
| load flake            | :: | nix-repl> :lf .                                            |
| find function in pkgs | :: | nix-repl> pkgs.writeT [Tab] -> makes pkgs.writeText        |
| find builtin function | :: | nix-repl> :doc builtins.isP [Tab] -> makes builtins.isPath |
|                       |    |                                                            |

** how to set pwd as a specific folder,
script = ''
  cd /home/hproxy/secrets
  ls -lah
  ${pkgs.su}/bin/su - hproxy -c "${inputs.agenix.packages.x86_64-linux.default}/bin/agenix -d /home/hproxy/secrets/wg-hproxy.age | ${pkgs.sudo}/bin/sudo ${pkgs.coreutils}/bin/tee /run/agenix.d/1/wg"
 '';

* folder management (authority, syncronize ...)
| change authority       | :: | $ sudo chown -R nginx:nginx /var/www/miso             |
| confirm authority list | :: | $ bat /etc/passwd                                     |
|                        |    |                                                       |
| syncronize folder      | :: | $ rsync -av --delete [PATH_source] [PATH_destination] |
|                        |    |                                                       |

* searching
| $ ls /nix/store [pl] grep [word] [pl] ws -l                                                           |    |                                         |   |   |
| $ echo ${}                                                                                            | :: | tab tab cursor inside the curly bracket |   |   |
|                                                                                                       |    |                                         |   |   |
| $ ls /nix/store [pl] grep nginx.conf [pl] xargs -I {} stat /nix/store/{} [pl] grep -E 'File[pl]Birth' | :: |                                         |   |   |
|                                                                                                       |    |                                         |   |   |

* remote connect
| xpra server start              | :: | $ xpra start :100 --start=xterm                                                                      |
| xpra remote server start       | :: | $ xpra start ssh://USER@HOST/ --start=xterm  https://github.com/Xpra-org/xpra#installation           |
| xpra attach (display in local) | :: | $ xpra attach ssh://USER@HOST/                                                                       |
|                                | :: | $ xpra attach tcp://IP:port                                                                          |
| vnc view                       | :: | $ vncviewer -geometry auto 192.168.13.40                                                             |
| scp                            | :: | $ scp -r auros@192.168.12.135:/home/auros/Downloads/test.jpg(file to send) ./Downloads(recieve path) |
| ssh jump                       | :: | $ ssh -J USER1@IP1(connecting PC) USER2@IP2(final target)                                            |
|                                |    |                                                                                                      |
| org-roam-ui in remote(xpra)    | :: | $ firefox localhost:35901                                                                            |
|                                |    |                                                                                                      |
