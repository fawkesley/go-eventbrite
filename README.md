# Go client for Eventbrite

[![GoDoc](https://godoc.org/apzuk/go-eventbrite?status.svg)](https://godoc.org/github.com/apzuk/go-eventbrite)

## Installation

To install the Go Client for Eventbrite API, please execute the following `go get` command.

```bash
go get github.com/apzuk/go-eventbrite
```

## Developer Documentation

View the [reference documentation](https://www.eventbrite.co.uk/developer/v3/quickstart/)

## Usage
   
    package main
    
    import (
        "fmt"
        "time"
    
        "github.com/apzuk/go-eventbrite"
    
        "golang.org/x/net/context"
    )
    
    func main() {
        clnt, _ := eventbrite.NewClient(
            eventbrite.WithToken(YOUR_TOKEN),
            eventbrite.WithRateLimit(2),
        )
    
        clnt.UserSetAssortments(context.Background(), "me", &eventbrite.UserSetAssortmentRequest{
            Plan: "package1",
        })
    
        res, _ := clnt.EventCreate(context.Background(), &eventbrite.EventCreateRequest{
            NameHtml: "Party!",
            DescriptionHtml: "Let's party tonight!",
            StartUtc: eventbrite.DateTime{
                Time: time.Now().AddDate(0,0,1),
            },
            StartTimezone: "Europe/London",
            EndUtc: eventbrite.DateTime{
                Time: time.Now().AddDate(0,0,3),
            },
            EndTimezone: "Europe/London",
            Currency: "GBP",
        })
    
        fmt.Printf("%+v", res)
    }

###Whoops, don't forget error handling!