# Go Rev.ai 
[![Go Report Card](https://goreportcard.com/badge/github.com/descriptinc/revai-go)](https://goreportcard.com/report/github.com/descriptinc/revai-go)
[![GoDoc](http://img.shields.io/badge/godoc-reference-blue.svg)](http://godoc.org/github.com/descriptinc/revai-go)

A [Rev.ai](https://rev.ai) Go client library.

## Installation

Install revai-go with:

```sh
go get -u github.com/descriptinc/revai-go
```

Then, import it using:

``` go
import (
    "github.com/descriptinc/revai-go"
)
```

## Documentation

For details on all the functionality in this library, see the [GoDoc](http://godoc.org/github.com/descriptinc/revai-go)
documentation.

Below are a few simple examples:

### New Client
```go
// default client
c := revai.NewClient("API-KEY")
```

### New Client With Options
```go
httpClient := &http.Client{
    Timeout: 30 * time.Second,
}

c := revai.NewClient(
    "API_KEY",
    revai.HTTPClient(httpClient),
    revai.UserAgent("my-user-agent"),
)
```

### Submit Local File Job

```go
params := &revai.NewFileJobParams{
	Media:    f, // some io.Reader
	Filename: f.Name(),
}

ctx := context.Background()

job, err := c.Job.SubmitFile(ctx, params)
// handle err

fmt.Println("status", job.Status)
```

### Submit Url Job

```go
const mediaURL = "https://support.rev.com/hc/en-us/article_attachments/200043975/FTC_Sample_1_-_Single.mp3"

params := &revai.NewURLJobParams{
    MediaURL: mediaURL, 
}

ctx := context.Background()

job, err := c.Job.SubmitURL(ctx, params)
// handle err

fmt.Println("status", job.Status)
```

### Caption

```go
params := &revai.GetCaptionParams{
	JobID: "job-id"
}

ctx := context.Background()

caption, err := c.Caption.Get(ctx, params)
// error check

fmt.Println("srt caption", caption.Value)
```

### Account

```go
ctx := context.Background()

account, err := c.Account.Get(ctx)
// error check

fmt.Println("balance", account.BalanceSeconds)
```

### Stream
[streaming example](examples/streaming/stream.go)
