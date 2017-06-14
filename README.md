dockerfiles
===========
本篇为docker学习，若有侵权请联系lc438732659@163.com，会立即删除。
感谢vimagick的 https://github.com/vimagick/dockerfiles 

## auto-completion

```bash
#!/bin/bash
#
# handy auto-completion for docker-exec
#

enter() {
  local name=${1:?}
  docker exec -it $name sh -c 'exec $(command -v bash || command -v sh)'
}

__enter() {
  local cur=${COMP_WORDS[COMP_CWORD]}
  for cid in $(docker ps -q)
  do
    local name=$(docker inspect -f '{{.Name}}' $cid)
    name=${name#/}
    if [[ $name = $cur* ]]
    then
      COMPREPLY+=("$name")
    fi
  done
}

complete -F __enter enter
```
