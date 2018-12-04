## Argument Parsing



```bash
PARAMS=""
while (( "$#" )); do
  case "$1" in # si esamina sempre il primo elemento in quanto viene fatto il pop 
  			   # degli elementi dell'array che coniente gli argomenti
    -f|--flag-with-argument)
      FARG=$2
      shift 2 # viene effettuato il pop degli argomenti dall'array
      ;;
    --) # end argument parsing
      shift
      break
      ;;
    -*|--*=) # unsupported flags
      echo "Error: Unsupported flag $1" >&2
      exit 1
      ;;
    *) # preserve positional arguments
      PARAMS="$PARAMS $1"
      shift
      ;;
  esac
done
# set positional arguments in their proper place
eval set -- "$PARAMS"
```

