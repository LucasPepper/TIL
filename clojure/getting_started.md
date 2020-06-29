# Getting Started

Requisites: JDK, Leiningen, VSCODE's extension for Clojure codes

1) Install JDK

```
sudo apt update
sudo apt install openjdk-13-jre-headless
```

2) Download Lein Script (in order to Leiningen to perform well)

```
cd /usr/local/bin
sudo wget https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein
ls
```

3) Give it permission to execute

```
sudo chmod +x lein
ls
./lein
```

If everything goes well, you should check the version with *lein -v*

4) Open the Lein's REPL (Read, Evaluate, Print, Loop) environment

```clojure
lein repl
"Hello Clojure!"
```

5) Search and install Calva extension or Clojure, Clojure-lint and Clojure Code

[Tutorial](https://medium.com/@chinnonsantos/clojure-no-visual-studio-code-vscode-com-nrepl-leiningen-linting-e-debug-397932305dd1)

[Clojure Docs](https://clojuredocs.org/)

[Clojure Exercises](https://4clojure.com)

[Exercism - Learning Clojure](https://exercism.io/tracks/clojure/learning)
