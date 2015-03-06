# engine-mode

`engine-mode` is a global minor mode for Emacs. It enables you to
easily define search engines, bind them to keybindings, and query them
from the comfort of your editor.

For example, suppose we want to be able to easily search GitHub:

```emacs
(defengine github
  "https://github.com/search?ref=simplesearch&q=%s")
```

This defines an interactive function `engine/search-github`. When
executed it will take the selected region (or prompt for input, if no
region is selected) and search GitHub for it, displaying the results
in your default browser.

The `defengine` macro can also take an optional key combination,
prefixed with `engine/keymap-prefix` (which defaults to "C-c /"):

```emacs
(defengine duckduckgo
  "https://duckduckgo.com/?q=%s"
  "d")
```

`C-c / d` is now bound to the new function `engine/search-duckduckgo`!
Nifty.

## Installation

`engine-mode` is available on MELPA.

You can also install it like any other elisp file by adding it to your
load path and globally enabling it:

```emacs
(require 'engine-mode)
(engine-mode t)
```

## Changing your default browser

`engine-mode` uses `browse-url` to open the URL it constructs. To
change the browser that `browse-url` uses, you'll need to redefine
the `browse-url-browser-function` variable.

For example, to use Emacs' built-in `eww` browser:

```emacs
(setq browse-url-browser-function 'eww-browse-url)
```

The implementation of the `browse-url-browser-function` variable
contains a comprehensive list of possible browsing functions. You can
get to that by hitting `C-h v browser-url-browser-function <RETURN>`
and following the link to `browse-url.el`.

## Importing keyword searches from other browsers

Since many browsers save keyword searches using the same format as
engine-mode (that is, by using `%s` in a url to indicate a search
term), it's not too hard to import them into Emacs.

@sshaw has written a script to [import from Chrome on OS X].

## Engine examples

```emacs
(defengine amazon
  "http://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=%s")

(defengine duckduckgo
  "https://duckduckgo.com/?q=%s"
  "d")

(defengine github
  "https://github.com/search?ref=simplesearch&q=%s")

(defengine google
  "http://www.google.com/search?ie=utf-8&oe=utf-8&q=%s"
  "g")

(defengine google-images
  "http://www.google.com/images?hl=en&source=hp&biw=1440&bih=795&gbv=2&aq=f&aqi=&aql=&oq=&q=%s")

(defengine google-maps
  "http://maps.google.com/maps?q=%s")

(defengine project-gutenberg
  "http://www.gutenberg.org/ebooks/search.html/?format=html&default_prefix=all&sort_order=&query=%s")

(defengine rfcs
  "http://pretty-rfc.herokuapp.com/search?q=%s")

(defengine stack-overflow
  "https://stackoverflow.com/search?q=%s")

(defengine twitter
  "https://twitter.com/search?q=%s")

(defengine wikipedia
  "http://www.wikipedia.org/search-redirect.php?language=en&go=Go&search=%s"
  "w")

(defengine wiktionary
  "https://www.wikipedia.org/search-redirect.php?family=wiktionary&language=en&go=Go&search=%s")

(defengine wolfram-alpha
  "http://www.wolframalpha.com/input/?i=%s")

(defengine youtube
  "http://www.youtube.com/results?aq=f&oq=&search_query=%s")
```

[import from Chrome on OS X]: https://gist.github.com/sshaw/9b635eabde582ebec442
