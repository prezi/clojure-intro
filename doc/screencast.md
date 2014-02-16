# Prerequisites

    brew install ttyrec # record terminal activity
    brew install links # text browser
    brew install tmux # terminal multiplexer
    brew install tree # directory listing

  - Set up terminal to 2x80 = 160 wide

# Install leiningen

You'll need a terminal and an editor.  The only Clojure-specific tool
you'll need is _leiningen_

    - `links http://leiningen.org`
    - Follow link to install
    - Quit _links_
    - Run `lein` to see the options

# The REPL

I spend half of my Clojure time in the REPL.

    - Run in any directory, you don't need a project
    - Readline support, tab-completion, C-r to search in history
    - Commands are functions: remember the parens
    - `(+ 2 3)`

# Clojure basics

(We are still in the REPL)
    
    - Everything is an expression
    - Comment
    - Parens and postfix, AST
    - Brackets and braces
    - String, keyword, symbol
        (first "str")
        (first '(this is a list))
        (first :kw)
    - `let`
    - `def`, `defn`
    - `map`, `filter`, `reduce`
    - `use`, `require`
        (require '[clojure.string :as string])
        (string/split "do me a favor" #" ") ; => ["do" "me" "a" "favor"]

        (use 'clojure.test)
        (is (= 3 (+ 2 2)))
    - `->`?
    - `(exit)` or C-d

# Set up a project and test it

    lein new foo
    cd foo
    tree
    lein test

# clojure.test
(Start with a split tmux, the upper half is taller, it's for the editor)
Let's go back to leiningen

    > lein test
    :b test/core_test.clj
    ; Fix test
    ; Add one more
    > lein test
    :b project.clj
    # or add `[cheshire "5.3.1"]`; json
    # :wq
    > lein repl # downloads unmet dependencies
    :b test/core_test.clj
    ; Add json encode/decode test
    user=> (require 'foo.core-test :reload)
    (is (thrown? IllegalArgumentException (first :keyword))) 
    (is (= \s (first "string")))
    (is (= 'symbols '(symbols parsed here)))
    (run-tests)
    user=> (require 'foo.core-test :reload)

    
# Testing with midje

  - Add midje dependency `[midje "1.6.2"]`
  - Rewrite test
