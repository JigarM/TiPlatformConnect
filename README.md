# Forked twitter-titanium
* Replaced jsOAuth-1.3.3
* twitter.js using jsOAuth.getAccessTokenKey() and jsOAuth.getAccessTokenSecret()
* Added tumblr.js using OAuth(not XAuth). Dose not change how to use twitter.js

```

twitter-titanium is a client-side Twitter library for Titanium Mobile. It simplifies the task of authenticating a user via Twitter. A backend is not required.
It's designed to emulate the API of the Facebook module included in Titanium Mobile.

It presents a very simple and straightforward API. You provide your OAuth configuration and simply call `authorize()`.
The user is prompted with a modal WebView to login to Twitter. After the user has logged in, the WebView disappears and a `login` event is fired.
Requests to Twitter's API endpoints are done with the `request()` function. We intentionally are not wrapping Twitter's API calls, this can
become a maintainence issue if Twitter updates it's API.

## How to use

There is an example app included in this repository. See [app.js](https://github.com/ebryn/twitter-titanium/blob/master/Resources/app.js).

```
var client = Twitter({
  consumerKey: "INSERT YOUR KEY HERE",
  consumerSecret: "INSERT YOUR SECRET HERE"
});

client.authorize(); // Pops up a modal WebView

client.addEventListener('login', function(e) {
  if (e.success) {
    // Your app code goes here... you'll likely want to save the access tokens passed in the event.
    
    // Here's an example API call:
    client.request("1/statuses/home_timeline.json", {count: 100}, 'GET', function(e) {
      if (e.success) {
        var data = JSON.parse(e.result.text);
      } else {
        alert(e.error);
      }
    });
  } else {
    alert(e.error);
  }
});
```

To use twitter-titanium in your app, download and copy the following files into your app:
[twitter.js](https://raw.github.com/ebryn/twitter-titanium/master/Resources/twitter.js)
[jsOAuth-1.3.1.js](https://raw.github.com/ebryn/twitter-titanium/master/Resources/jsOAuth-1.3.1.js)

## Nice features

- Android compatible and tested!
- On iOS, a back button is displayed if the user does any navigation within the WebView. For example, if the user clicks the forgot password link.

## Thanks

- twitter-titanium uses the [jsOAuth](github.com/bytespider/jsOAuth) library by @bytespider
- [Metamorph.js](https://github.com/tomhuda/metamorph.js) by @wycats and @tomdale for inspiration

## Contact

twitter-titanium was written by Erik Bryn. You can find him on Twitter at @ebryn.
