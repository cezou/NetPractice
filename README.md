# NetPractice

#### _This project is a general practical exercise to let you discover networking._

## I made an zsh shortcut with _"bc"_ : bconv

_because the subject allows us to use the bc command._

#### It converts a CIDR mask to a dotted decimal mask

```bash
function bconv() {
	echo "$1" |
	awk '{
		for(i=1; i<=32; i++)
		{
			printf i<=$1 ? "1" : "0";
			if(i%8==0) printf "\n";
		}
	}' |
	while IFS= read -r binary; do
		echo -n "$(echo "ibase=2; $binary" | bc)."
	done |
	sed 's/\.$/\n/'
}
```

### Usage:

Paste the command above in your ~/.zshrc file and restart your terminal

```bash
$ bconv 30
255.255.255.252
```
