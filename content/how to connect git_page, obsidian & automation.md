---
title: this is test2!
---
#index
[[index]]

# 1. git_page
## a. make git repository
### fork & setting 'quartz' repo
> [!NOTE] fork & setting 'quartz' repo
> 1. fork https://github.com/jackyzha0/quartz
> 2. make local folder for setting nix flake dev shell (ex. /gits/quartz_gitPage/)
> 3. make a flake file that makes dev shell of nodejs
> 4. make a .envrc in the same folder
> 5. $direnv allow (for auto adopt of dev shell environment when open /gits/quartz_gitPage/)
> 6. instead of 4,5 -> $nix develop
> 7. /gits/quartz_gitPage/$ git clone https://github.com/syryuauros/syryuauros.github.io.git
> 8. 

### flake.nix
```
  outputs = input@{self, nixpkgs, flake-utils, ...} :

    flake-utils.lib.eachSystem [ "x86_64-linux" ] (system:
      let

        pkgs = import nixpkgs {
          inherit system;
        };

      in rec {
        packages.nodeJs = pkgs.nodejs_20;
        packages.corepack = pkgs.corepack;
        defaultPackage = packages.nodeJs;

        devShells.default = pkgs.mkShell rec {
          name = "nodeJs";
          buildInputs = [
            packages.nodeJs
            packages.corepack
            ];

        };

      });
```

### .envrc
```
use flake
```

## b. gitPage setup
### basic setup for quartz
https://quartz.jzhao.xyz/
### gitPage setup for quartz
https://quartz.jzhao.xyz/hosting
![[Pasted image 20250306134433.png]]

### 참조, github page static version (branch direct sourcing)
https://phodobit.kr/49

## c. auto update for git Page
### git hook 사용
- /gits/quartz_gitPage/syryuauros.github.io/.git/hooks/pre-push
-  .git folder is not shown in doom emacs merely 'Shift + h' 
- use cmd ->  /gits/quartz_gitPage/syryuauros.github.io/$ ls -la
- or spc-f-f in doom emacs (doom/find-file-in-private-config)
- edit 'pre-push.sample' to use 'npx quartz sync' -> change file name to 'pre-push' to activate hook
- without exit code (if phrase for flags) it makes a loop because 'npx quartz sync' also include 'git push'

```
remote="$1"
url="$2"

zero=$(git hash-object --stdin </dev/null | tr '[0-9a-f]' '0')

while read local_ref local_oid remote_ref remote_oid
do
	if test "$local_oid" = "$zero"
	then
		# Handle delete
		:
	else
		if test "$remote_oid" = "$zero"
		then
			# New branch, examine all commits
			range="$local_oid"
		else
			# Update to existing branch, examine new commits
			range="$remote_oid..$local_oid"
		fi

		# Check for WIP commit
		commit=$(git rev-list -n 1 --grep '^WIP' "$range")
		if test -n "$commit"
		then
			echo >&2 "Found WIP commit in $local_ref, not pushing"
			exit 1
		fi
	fi
done

if [ -f ./.git/hooks/.quartz-synced  ]; then
	echo "Quartz sync already ran. Skipping..."
	rm ./.git/hooks/.quartz-synced
	exit 0
fi

touch ./.git/hooks/.quartz-synced

echo "Running Quartz Sync..."
npx quartz sync

exit 0

```

