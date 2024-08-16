# NetPractice

#### _This project is a general practical exercise to let you discover networking._

## I made zsh shortcuts with _"bc"_
_because the subject allows us to use the bc command._

### ↪ Functions DDM and CIDR
_"ddm" converts a cidr mask to a dotted decimal mask, and "cidr" the inverse_

```bash
function ddm()
{
	cidr="$1"
	res=""
	for i in {1..4}; do
		if (( cidr >= 8 )); then
			res+="255"
			cidr=$((cidr - 8))
		else
			res+=$(echo "256 - 2^(8 - $cidr)" | bc)
			cidr=0
		fi
		(( i < 4 )) && res+="."
	done
	echo "$res"
}

function cidr()
{
	echo "$1" | awk -F '.' '{
		n = 0
		for (i = 1; i <= NF; i++) {
			cmd = "echo " $i " | bc"
			cmd | getline byte
			close(cmd)
			while (byte > 0) {
				n += byte % 2
				byte = int(byte / 2)
			}
		}
		print n
	}'
}
```

### Usage:
- Install [Ohmyzsh](https://ohmyz.sh/#install)
- Paste the code above in your ~/.zshrc file then restart your terminal

```bash
$ ddm 30
255.255.255.252

$ cidr 255.255.255.252
30
```
