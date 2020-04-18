# nebula-go

![build status](https://github.com/vesoft-inc/nebula-go/workflows/build/badge.svg)

Official Nebula Go client which communicates with the server using [fbthrift](https://github.com/facebook/fbthrift/).

Please be careful do not to modify the files in the graph directory, these codes were all generated by fbthrift.

## Install

```shell
$ go get -u -v github.com/vesoft-inc/nebula-go
```

## Usage example

```go
package main

import (
  "log"

  nebula "github.com/vesoft-inc/nebula-go"
  graph "github.com/vesoft-inc/nebula-go/nebula/graph"
)

func main() {
  client, err := nebula.NewClient("127.0.0.1:3699")
  if err != nil {
    log.Fatal(err)
  }

  if err = client.Connect("username", "password"); err != nil {
    log.Fatal(err)
  }
  defer client.Disconnect()

  resp, err := client.Execute("SHOW HOSTS;")
  if err != nil {
    log.Fatal(err)
  }
  
  if resp.GetErrorCode() != graph.ErrorCode_SUCCEEDED {
    log.Printf("ErrorCode: %v, ErrorMsg: %s", resp.GetErrorCode(), resp.GetErrorMsg())
  }
  
}
```
