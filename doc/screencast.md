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
