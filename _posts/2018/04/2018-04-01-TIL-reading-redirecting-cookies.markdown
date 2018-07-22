---
layout: post
title:  "TIL: Consuming Data, Redirects, and Cookies"
date:   2018-04-01 21:00:00 -0000
categories:
  - Coding
tags:
  - golang
---
Worked on some more web development with Go training today, worked through several scenarios worth noting, specifically dealing with data passed in via forms/url, handling redirects, and basic cookie activies

## Consuming Data From Forms/URL
GO makes it super simple for parsing values passed in via a URL query string. To do so, all you need to do is use the `http.FormValue()` method, passing in the name of the parameter you want to get the value for.

For example, if a query string looks like `http://mysite.com/?apple=pie&color=red`, we could grab the vales of `apple` and `color` by creating a function that does the following:

```golang
func foo(w http.ResponseWriter, r *http.Request) {
	a := r.FormValue("apple")
	c := r.FormValue("color")
	io.WriteString(w, "apple: "+a+", color: "+c)
}
```

The same method is used for retrieving the values from `<form>` submissions. In the html of the form, the fields will have `name=value` tags. That name is what will be used inside of the `http.FormValue("value")` method.

## Redirects
I've never actually worked with the 3XX range of http codes at work, so this was some new hands stuff for me. The three 3xx codes that were covered in this section were 301 (moved permanently), 303 (see other), and 307 (temporary move).

There are two ways of coding the redirect. The first way is the manual way, where you can set a `Location` header as well as the response code using the `http.ResponseWriter.Header().Set()` method:

```golang
func bar(w http.ResponseWriter, r *http.Request) {
	fmt.Print("Your request method at bar: ", r.Method, "\n\n")
	w.Header().Set("Location", "/")
	w.WriteHeader(http.StatusSeeOther)
}
```

But theres an easier way of doing this in a single step. Here's the exact same thing using the `http.Redirect()` method:

```golang
func bar(w http.ResponseWriter, r *http.Request) {
	fmt.Print("Your request method at bar: ", r.Method, "\n\n")
	http.Redirect(w, r, "/", http.StatusSeeOther)
}
```

I like this second way, it's much cleaner.

## Cookies
This was actually my first time working with cookies. I knew that cookies were used for some sort of tracking activity but I didn't know for exactly what.

Cookies are used to store information about the user and their session information. The user has to allow cookies in order for them to be stored. Cookies are used within the browser and are only sent to the domain that they correspond with.

In Go, cookies are set using the `http.SetCookie` method, by passing in a cookie struct (can lookup what that is). Here's how you'd set it:

```golang
func set(w http.ResponseWriter, r *http.Request) {
	http.SetCookie(w, &http.Cookie{
		Name:  "my-cookie",
		Value: "some value",
	})
	fmt.Fprintln(w, "Cookie written - Check your browser!")
}
```

To then read this back from the browser, you can grab the `Cookie` parameter of the `http.Request` passed in:

```golang
func read(w http.ResponseWriter, r *http.Request) {
	c, err := r.Cookie("my-cookie")
	if err != nil {
		http.Error(w, err.Error(), http.StatusBadRequest)
		return
	}
	fmt.Fprintln(w, "Your cookie:", c)
}
```

Cookies are then good until they expire. They're usually created with `MaxAge` values. In fact, the way that you'd delete a Cookie is by setting it's MaxAge to -1.