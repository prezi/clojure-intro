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

    => ; Data
    => 42
    => 0.3333333
    => 1/3
    => "some text"
    => :keyword
    => true
    => false
    => nil
    => [1 2 4]
    => ["mixed vector" :of 4 "entries"]
    => {:eyes 2, :fingers 20}
    => {:lucky-numbers [3 7 9], :unlucky-numbers [4 13]}
    => #{:set :of :keywords :of :keywords}
    => #"regex.*"
    => #"("
    => (def pi 3.14)
    => pi
    => (def xs [2 3 5 8])
    => xs
    => (let [local-pi pi] local-pi)
    => (let [pi 3] pi)
    => pi
    => (let [local-pi 3
             pi local-pi]
         pi)
    => pi

    => ; Call a function: (function arg1 arg2 ...)
    => (- 5 3)
    => (max 0 (min 1 2))
    => (= 3 4)
    => (= {:eyes 2, :fingers 20} {:fingers 20, :eyes 2})
    => (if true :truthy :FALSEY)
    => (if false :truthy :FALSEY)
    => (if nil :truthy :FALSEY)
    => (if :anything-else :truthy :FALSEY)
    => (if 42 :truthy :FALSEY)
    => (if 0 :truthy :FALSEY)
    => (if [] :truthy :FALSEY)
    => (if {} :truthy :FALSEY)
    => (when true :truthy)
    => (when false :truthy)
    => (when nil :truthy)
    => xs
    => (first xs)
    => (rest xs)
    => (count xs)
    => (reverse xs)
    => (take 2 xs)
    => (drop 2 xs)
    => (filter odd? xs)
    => (remove odd? xs)
    => (every pos? xs)
    => (some even? xs)
    => (map inc xs)
    => (apply max xs)
    => (reduce + [1 2 3])

    => ; lambda 
    => (fn [x] (+ x 1))
    => ((fn [x] (+ x 1)) 42)
    => (map (fn [x] (+ x 1)) [2 4])
    => (def inc' (fn [x] (+ x 1)))
    => (inc' 42)
    => (map inc' [2 4])
    => (defn inc-simpler [x] (+ x 1))
    => (inc-simpler 42)
    => (defn avg [x y] (/ (+ x y) 2))
    => avg
    => (avg 3 5)
    => (avg 3 5 1)
    => (defn avg [& rest-args] (/ (reduce + rest-args) (count rest-args))) 
    => (avg 3 5 1)

    => ; deep structures
    => (def me {:eyes 2, :fingers 20, :name {:first "Jack"}, :numbers [7 13]}
    => (get me :eyes)
    => (get me :tail)
    => (get me :tail :invisible)
    => (me :eyes)
    => (get me :name)
    => (get-in me [:name :first])
    => (get-in me [:tail :no-NPE])
    => (get-in me [:numbers 0])
    => (get-in me [:numbers 2])
    => (-> me :name)
    => (-> me :name :first)
    => (-> me :name :first first)
    => (-> me :fingers inc)
    => (-> me :fingers (- 2))
    => (assoc me :nose 1)
    => (assoc me :name "Jack the Ripper")
    => (assoc-in me [:name :family] "the Ripper")
    => (assoc-in me [:name first] "Jack")

    => ; namespaces
    => (def x 42)
    => x
    => (ns foo.bar)
    => x
    => (def x 999)
    => (ns user)
    => x
    => (ns foo.bar (:require [clojure.string :as string]))
    => (string/trim "  abc\n  ")
    => (string/upper-case "abc")
    => (string/split "jack, mary, john" #", *")
    => (-> "  bookkeeper  " string/trim string/upper-case (string/split #"E+"))
    => union
    => (ns foo.bar (:use clojure.set))
    => union
    => (union #{3 4} #{4 5})
    => (ns foo.bar (:use [clojure.data :only [diff]]))
    => (diff #{3 4 5} #{4 5 6})

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
