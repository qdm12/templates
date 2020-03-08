# SH

This contains a bunch of tricky/useful commands and functions compatible with `/bin/sh`.

```sh
# Wget/Tar/File Pipe
wget -qO- https://example.com/mybin.gz | tar -xOz > /usr/local/mybin
# Default variable
X=${X:-hello}
# Test read access
test -r file.txt
[ $? = 0 ] || echo "Can't read file.txt"
# Test variable is a number
[ ! -z $(echo $x | grep -E '^[0-9]+$') ]
# Checksum verification
echo "${CHECKSUM} filepath" | sha256sum -c -
# Echo in red to stderr
2>&1 echo -e "\033[0;31m####################### NOTICE #######################\033[0m"
# Run commands without root (I guess?)
exec su-exec -e sh <<EOF
# my commands here
EOF
```

Shell functions:

```sh
exitOnError(){
  # $1 must be set to $?
  status=$1
  message=$2
  [ "$message" != "" ] || message="Error!"
  if [ $status != 0 ]; then
    printf "$message (status $status)\n"
    exit $status
  fi
}

exitIfUnset(){
  # $1 is the name of the variable to check - not the variable itself
  var="$(eval echo "\$$1")"
  if [ -z "$var" ]; then
    printf "Environment variable $1 is not set\n"
    exit 1
  fi
}

exitIfNotIn(){
  # $1 is the name of the variable to check - not the variable itself
  # $2 is a string of comma separated possible values
  var="$(eval echo "\$$1")"
  for value in ${2//,/ }
  do
    if [ "$var" = "$value" ]; then
      return 0
    fi
  done
  printf "Environment variable $1=$var must be one of the following: "
  for value in ${2//,/ }
  do
    printf "$value "
  done
  printf "\n"
  exit 1
}
```
