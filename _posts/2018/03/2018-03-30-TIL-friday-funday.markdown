---
layout: post
title:  "TIL: Friday Funday"
date:   2018-03-30 17:00:00 -0500
categories: TIL
---
Day off from work meant it mostly a day of relaxation. Lots of being lazy, falling down Youtube holes, and playing some video games. But I also ended up doing a bit more work with studying Golang.

Today should be pretty short, so let's get on to it.

## Serving Files in Go Web Servers
There's a few different ways that you can serve up static files using Go's `http` library. The lesson I went over today covered 4 methods, one one of which is actually recommended.

### 1. Using `io.Copy()`
You can literally copy the data from a file and place it into the response message that goes back to the user. This is obviously not a great way of doing things as you have to open the file, copy it's contents out, close the file, and send the message back. No thanks.

```golang
package main

import (
	"io"
	"net/http"
	"os"
)

func main() {
	http.HandleFunc("/", dog)
	http.HandleFunc("/toby.jpg", dogPic)
	http.ListenAndServe(":8080", nil)
}

func dog(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "text/html; charset=utf-8")
	io.WriteString(w, `
		<img src="toby.jpg">
		`)
}

func dogPic(w http.ResponseWriter, r *http.Request) {
	f, err := os.Open("toby.jpg")
	if err != nil {
		http.Error(w, "file not found", 404)
		return
	}
	defer f.Close()

	io.Copy(w, f)
}
```

### 2. `http.ServeContent()`
Not really that much of a step up from the `io.Copy()` option, this one requires that you still open the file and get it's contents out only to turn around and serve it's values. Still pretty meh, and only works with one file at a time.

```golang
package main

import (
	"io"
	"net/http"
	"os"
)

func main() {
	http.HandleFunc("/", dog)
	http.HandleFunc("/toby.jpg", dogPic)
	http.ListenAndServe(":8080", nil)
}

func dog(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "text/html; charset=utf-8")
	io.WriteString(w, `
		<img src="toby.jpg">
		`)
}

func dogPic(w http.ResponseWriter, r *http.Request) {
	f, err := os.Open("toby.jpg")
	if err != nil {
		http.Error(w, "file not found", 404)
		return
	}
	defer f.Close()

	fi, err := f.Stat()
	if err != nil {
		http.Error(w, "file not found", 404)
		return
	}
	http.ServeContent(w, r, f.Name(), fi.ModTime(), f)
}
```
### 3. `http.ServeFile`
Now we're getting closer. `http.ServeFile` allows you to specify the file that you want opened up, but it still requires that you have extra routing to get to the file path. So close, but still not what we want:

```golang
package main

import (
	"io"
	"net/http"
)

func main() {
	http.HandleFunc("/", dog)
	http.HandleFunc("/toby.jpg", dogPic)
	http.ListenAndServe(":8080", nil)
}

func dog(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "text/html; charset=utf-8")
	io.WriteString(w, `
		<img src="toby.jpg">
		`)
}

func dogPic(w http.ResponseWriter, r *http.Request) {
	http.ServeFile(w, r, "toby.jpg")
}
```

### 4. `http.FileServer()`
Here we go, this is what we want. `http.FileServer()` allows you to host an entire directory of files like you would want to. Rather than using `http.HandleFunc()` and passing in a function, we just use `http.Handle()` with the path and the `http.FileServer()` pointing at the directory. We can also get fancy and add in stripping loggic to redirect the resources path:

```golang
package main

import (
	"io"
	"net/http"
)

func main() {
	http.Handle("/resources/", http.StripPrefix("/resources", http.FileServer(http.Dir("./assets"))))
	http.HandleFunc("/", dog)
	http.ListenAndServe(":8080", nil)
}

func dog(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "text/html; charset=utf-8")
	io.WriteString(w, `
		<img src="/resources/toby.jpg">
		`)
}
```

## Aubery Plaza's ASMR Interview
ASMR is a wonderful thing. If you've never experienced before, or don't get the tingles, my heart goes out to you. Over the last year or so I've realy leveraged it's effects to calm down when I'm having a bad day or to start the day off on a more positive note.

Add in someone hilarious like Aubery and it's even more amazing. Please watch and enjoy your tingles:

<iframe width="560" height="315" src="https://www.youtube.com/embed/MXaBom7KKmU?rel=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>