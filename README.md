# tl

Package tl implements TL (Type Language) schema parser and writer.
Inspired by [grammers](https://github.com/Lonami/grammers) parser.

```console
go get github.com/ernado/tl
```

## Example

This program parses schema from stdin and prints all definitions with their
names and types.

```go
package main

import (
	"fmt"
	"os"

	"github.com/ernado/tl"
)

func main() {
	schema, err := tl.Parse(os.Stdin)
	if err != nil {
		panic(err)
	}
	for _, d := range schema.Definitions {
		fmt.Printf("%s#%x = %s;\n", d.Definition.Name, d.Definition.ID, d.Definition.Type)
	}
}
```

You can use like that:
```console
$ curl -s "https://raw.githubusercontent.com/tdlib/td/master/td/generate/scheme/td_api.tl" \
    | go run github.com/ernado/tl/cmd/tl-print \
    | less
```

Output:
```tl
double#2210c154 = Double;
string#b5286e24 = String;
int32#5cb934fa = Int32;
int53#6781c7ee = Int53;
int64#5d9ed744 = Int64;
bytes#e937bb82 = Bytes;
boolFalse#bc799737 = Bool;
boolTrue#997275b5 = Bool;
error#9bdd8f1a = Error;
ok#d4edbe69 = Ok;
tdlibParameters#d29c1d7b = TdlibParameters;

//...
```
