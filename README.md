# fastjson: optimized standard library JSON for Go

`fastjson` has the same API as json from standard library `encoding/json`. 
Only thing it differs from `encoding/json` is `Unmarshal` and `Decode` functions. They are faster.

## Getting Started
go get github.com/intel-go/fastjson

##Perfomance
It depends on the content of your json structures, not the structure you parse to.
* if `.json` has a lot of strings or numbers, fastjson is **2x** quicker, than `encoding/json`
* otherwize fastjson is `1.5x` quicker, than `encoding/json`

##Example
```Go
import (
    "github.com/intel-go/fastjson"
    "fmt"
)

func main() {
    var jsonBlob = []byte(`[
	{"Name": "Platypus", "Order": "Monotremata"},
	{"Name": "Quoll",    "Order": "Dasyuromorphia"}
    ]`)
    type Animal struct {
	Name  string
	Order string
    }
    var animals []Animal
    err := fastjson.Unmarshal(jsonBlob, &animals)
    if err != nil {
	fmt.Println("error:", err)
    }
    fmt.Printf("%+v", animals)
    // Output:
    // [{Name:Platypus Order:Monotremata} {Name:Quoll Order:Dasyuromorphia}]
}
```
##API
API is the same as in encoding/json
[GoDoc](https://golang.org/pkg/encoding/json/#Unmarshal)
