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
    - `let`
    - `def`, `defn`
    - `map`, `filter`, `reduce`
    - `use`, `require`
    - `->`?
    - `(exit)` or C-d

# Set up a project

Let's go back to leiningen

    lein new foo
    tree foo
    cd foo
    vim project.clj
    # Add midje dependency `[midje "1.6.2"]`
    # :wq
    lein repl # downloads unmet dependencies
    
