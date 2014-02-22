# Prerequisites

    brew install ttyrec # record terminal activity
    brew install links # text browser
    brew install tmux # terminal multiplexer
    brew install tree # directory listing

    brew install sox # sound recording
    brew install libogg

    # To add fancy captions
    brew install figlet
    brew install toilet

    rm ~/bin/lein
    mv ~/.lein /tmp
    rm -rf /tmp/any_directory
    chsh
    bash
    reset

    # toilet -F border -F gay "Clojure basics"
    # cowsay -f turtle "Clojure basics"

# Setting the table

    cowsay -f bud-frogs "Setting the table"

## Install leiningen

    # Download and install leiningen
    # That's the only Clojure-specific tool you'll need
    links leiningen.org
    (Follow link to install)
    (Click download)
    `Esc -> v` (Save as)
    (Enter `~/bin/lein`)
    `q` (Quit)
    chmod a+x ~/bin/lein
    lein

## The REPL

    # I spend half of my Clojure time in the REPL
    mkdir /tmp/any_directory
    cd /tmp/any_directory
    lein repl
    => ; Welcome to the REPL
    => ; It has tab-completion
    => *<Tab>c<Tab>l<Tab><Enter>
    => ; Search in history with C-r
    => <C-r>cl<Enter>
    => (help)
    => ; Always remember those lisp-y parens!
    => (quit)

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

## Set up a project and test it

    lein new foo
    cd foo
    tree
    lein test

## clojure.test
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

    
## Testing with midje

  - Add midje dependency `[midje "1.6.2"]`
  - Rewrite test
