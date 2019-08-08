## Function: Man to Pdf



``` bash
pman()
{
 PMANPATH="/tmp/$UID-$1-man"
 man -t $1 > "$PMANPATH.ps"
 ps2pdf "$PMANPATH.ps" "$PMANPATH.pdf"
 evince "$PMANPATH.pdf" &
}
```

