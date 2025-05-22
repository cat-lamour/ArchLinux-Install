# ArchLinux Install
HowTos, Guides, Scripts, and more.




## Basic Install


### Check for tools
```
pass=true

tools[0]=$(which wget)
tools[1]=$(which b2sum)
tools[2]=$(which gpg)

for tool in ${tools[@]}; do
    if [ $tool -ne 0 ]; then
        pass=false
    fi
done

if [ pass == 'true' ]; then
    echo 'All tools present. Proceed.'
else
    echo 'Missing something deep within your soul. Ensure toolchain is installed.'
fi
```
