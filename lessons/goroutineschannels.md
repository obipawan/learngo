---
layout: default
---

# Goroutines

A goroutine is a lightweight thread of execution. Go has rich support for concurrency using goroutines and channels.
To create a goroutinee use the `go` keyword followed by a function invocation.

```go
func foo() {
    fmt.Println("this will run concurrently")
}

func main () {
    go foo() // runs concurrently
    fmt.Scanln() //waits for user input
}
```

# Channels

Channels provide a way for two goroutines to communicate with one another and synchronize their execution.

Create a new channel with `make(chan val-type)`. Channels are typed by the values they convey.

```go
stringChannel := make(chan string)

go func() {
    stringChannel <- "hello world"
}()

msg := <- stringChannel
fmt.Println(msg)
```

Send a value into a channel using the `channel <-` syntax. Here we send `"hello world"` to the `stringChannel` we made above, from a new goroutine.

The `<-channel` syntax receives a value from the channel. Here we’ll receive the `"hello world"` message we sent above and print it out.

By default sends and receives block until both the sender and receiver are ready. This property allowed us to wait at the end of our program for the `"hello world"` message without having to use any other synchronization.

## Channel Buffering

By default channels are unbuffered, meaning that they will only accept sends (`chan <-`) if there is a corresponding receive (`<- chan`) ready to receive the sent value. Buffered channels accept a limited number of values without a corresponding receiver for those values.

```go
bufferedChannel := make(chan string, 2) // channel of strings buffering up to 2 values

go func() {
    bufferedChannel <- "hello"
    bufferedChannel <- "world"
}()

fmt.Println(<- bufferedChannel) // hello
fmt.Println(<- bufferedChannel) // world
```

## Channel Synchronization

We can use channels to synchronize execution across goroutines.

```go
func worker (doneChannel chan bool) {
    fmt.Println("workering..")
    time.Sleep(time.Second)
    fmt.Println("done")
    doneChannel <- true // Send a value to notify that we’re done.
}

func main () {
    doneChannel := make(chan bool)
    go worker(doneChannel)
    <- doneChannel  // Block until we receive a notification from the worker on the channel.
}
```

The `doneChannel` will be used to notify another goroutine that this function’s work is done.

## Channel Direction

When using channels as function parameters, you can specify if a channel is meant to only send or receive values. This specificity increases the type-safety of the program.

```go

func ping(pings chan<- string, msg string) {
	pings <- msg
}

func pong(pings <-chan string, pongs chan<- string) {
	pongs <- <-pings
}

func main() {
	pings := make(chan string, 1)
	pongs := make(chan string, 1)
	ping(pings, "passed message") // sends message over to pings channel
	pong(pings, pongs)            // pulls message from pings and sends it over to pongs channel
	fmt.Println(<-pongs)          // pulls message from pongs channel
}
```

## Select

Go’s select lets you wait on multiple channel operations. Combining goroutines and channels with select is a powerful feature of Go.

```go
c1 := make(chan string)
c2 := make(chan string)
go func() {
    time.Sleep(1 * time.Second)
    c1 <- "one"
}()
go func() {
    time.Sleep(2 * time.Second)
    c2 <- "two"
}()
for i := 0; i < 2; i++ {
    select {
    case msg1 := <-c1:
        fmt.Println("received", msg1)
    case msg2 := <-c2:
        fmt.Println("received", msg2)
    }
}
```

The total execution time is only ~2 seconds since both the 1 and 2 second Sleeps execute concurrently.

## Timeouts

Timeouts are important for programs that connect to external resources or that otherwise need to bound execution time. Implementing timeouts in Go is easy and elegant thanks to channels and select.

```go
c1 := make(chan string)
go func() {
    time.Sleep(2 * time.Second)
    c1 <- "result 1"
}()

select {
case res := <-c1:
    fmt.Println(res)
case <-time.After(time.Second):
    fmt.Println("timeout c1")
}
```
Here’s the select implementing a timeout. `res := <-c1` awaits the result and `<-Time.After` awaits a value to be sent after the timeout of 1s. Since select proceeds with the first receive that’s ready, we’ll take the timeout case if the operation takes more than the allowed 1s.

## Non-Blocking Channels

Basic sends and receives on channels are blocking. However, we can use select with a default clause to implement non-blocking sends, receives, and even non-blocking multi-way selects.

```go
messages := make(chan string)
signals := make(chan bool)

select {
case msg := <-messages:
    fmt.Println("received message", msg)
default:
    fmt.Println("no message received")
}

msg := "hi"
select {
case messages <- msg:
    fmt.Println("message sent", msg)
default:
    fmt.Println("no message sent")
}
```

## Closing Channels

Closing a channel indicates that no more values will be sent on it. This can be useful to communicate completion to the channel’s receivers.

```go
jobs := make(chan int, 5)
done := make(chan bool)
go func() {
    for {
        job, more := <-jobs
        if more {
            fmt.Println("received job", job)
        } else {
            fmt.Println("received all jobs")
            done <- true
            return
        }
    }
}()

for j := 0; j < 3; j++ { // This sends 3 jobs to the worker over the jobs channel, then closes it.
    jobs <- j
    fmt.Println("sent job", j)
}
close(jobs)
fmt.Println("sent all jobs")
<-done
```

## Range over channels

`Range` iterates over each element as it’s received from queue. If we closed the channel, the iteration terminates after receiving the elements.

```go
msgChannel := make(chan string, 10)
msgChannel <- "one"
msgChannel <- "two"
msgChannel <- "three"
close(msgChannel)

for item := range msgChannel {
    fmt.Println(item)
}
```