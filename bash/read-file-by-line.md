## Read File line by line



```bash
while IFS='' read -r line || [[ -n "$line" ]]; do
	echo $line
done < "$FILE"
```

- `IFS=''` (or `IFS=`) prevents leading/trailing whitespace from being trimmed.
- `-r` prevents backslash escapes from being interpreted.
- `|| [[ -n $line ]]` prevents the last line from being ignored if it doesn't end with a `\n` (since `read` returns a non-zero exit code when it encounters EOF).

