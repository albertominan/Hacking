Gestión de entornos y sistemas:

    $0
    lsb_release -a
    uname -a

Gestión de archivos y directorios:

    grep -E "^user|^root"
    grep -v root
    cat ejemplo.txt | wc -l
    diff passwords.new passwords.old
    cat /etc/shells
    lsattr ejemplo.txt
    chattr -i -V ejemplo.txt
    find -perm -4000 2>/dev/null
    find .
    find . -type f -printf "%f\t%p\t%u\t%g\t%m\n" | column -t
    find . -name .hidden
    find . -name .hidden | xargs cat
    find . -name .hidden | xargs grep "leaving"
    find . -type f -readable ! -executable -size 1033c | xargs cat
    find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
    cat $(find . -name -file07)

Gestión de procesos y privilegios:

    pwdx 39609
    export PATH=<PATH>
    watch -n 1 ls -l /bin/bash
    bash -p
    disown
    disown -a
    firefox > /dev/null 2>&1 &

Gestión de texto y datos:

    awk '/ejemplo/' ejemplo.txt | awk '{print $1}'
    grep "millionth" data.txt -n
    awk 'NR==1994' ejemplo.txt
    awk 'NF{print $NF}'
    cat data.txt | sort | uniq -u
    strings data.txt | grep "===" | tail -n 1
    tr ' ' '\n'
    tr 'r' 'o'
    cat data.txt | tr '[G-ZA-Fg-za-f]' '[T-ZA-St-za-s]'
    echo "Hola que tal" | xxd
    echo "Hola que tal" | xxd -ps
