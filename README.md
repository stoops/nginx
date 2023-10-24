# nginx

```
./configure --without-http_rewrite_module --with-threads --with-stream --with-stream_ssl_preread_module --with-select_module --with-poll_module
make
```

# macos

```
addr="$1"
port="$2"
if [ "$addr" != "" -a "$port" != "" ] ; then
  conn=$(/sbin/pfctl -ss 2>/dev/null | /usr/bin/tr '<\->\t' ' ' | /usr/bin/grep -i " ${addr}:${port} " | /usr/bin/awk '{ print $4 }' | /usr/bin/head -n 1 | /usr/bin/tr
d '\r\n')
  echo -n "${conn}"
fi
exit 0
```

# linux

```
addr="$1"
port="$2"
if [ "$addr" != "" -a "$port" != "" ] ; then
  conn=$(cat /proc/net/nf_conntrack | sed -e 's/packets=/~/g' | tr '~' '\n' | grep -i " src=${addr} .* sport=${port} " | sed -e 's/^.* dst=\([^ ]*\) .* dport=\([^ ]*\)
*$/\1:\2/')
  echo -n "${conn}"
fi
exit 0
```
