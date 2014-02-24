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
(See also http://www.cis.upenn.edu/~matuszek/Concise%20Guides/Concise%20Clojure.html)

    => ; What you'd expect
    => 42
    => "some text"
    => [1 2 4]
    => ["mixed vector" "of" 4 "entries"]
    => {"eyes" 2, "fingers" 10}
    => ; Call a function: (function arg1 arg2 ...)
    => (- 5 3)
    => (first [2 4 8])
    => (max 0 (min 1 2))
    => ; Define
    => (def pi 3.14)
    => pi
    => (let [pi 3.1415926] pi)
    => (let [r 2
             pi 3.1415926]
         (* r r pi))
    => (let [a 1
             dummy (println "interim" a)
             a (* 2 a)]
          a)
    => (def xs [2 3 5 8])
    => (count xs)
    => (rest xs)
    => (reverse xs)
    => (take 2 xs)
    => (drop 2 xs)
    => (filter odd? xs)
    => (remove odd? xs)
    => (map inc xs)
    => (apply max xs)
    => (reduce + [1 2 3])
    => ; lambda 
    => (fn [x] (+ x 1))
    => ((fn [x] (+ x 1)) 42)
    => (def inc' (fn [x] (+ x 1)))
    => (inc' 42)
    => (map inc' [2 4])
    => (defn avg [x y] (/ (+ x y) 2))
    => avg
    => (avg 3 5)
    => (avg 3 5 1)

    => ; The & sign denotes rest args
    => (defn avg [& xs] (/ (reduce + xs) (count xs))) 
    => (avg 3 5 1)

    => (map #(+ % 1) [2 4]) ; shortcut
    => ; comma is treated as whitespace, it's used to improve readability
    => [1,,,2],,,
    
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
