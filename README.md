# TIL

> Today I Learned

A collection of concise write-ups on small things I learn day to day across a
variety of languages and technologies. These are things that don't really
warrant a full blog post.


_5 TILs and counting..._

---

### Categories

* [Md](#MD)
* [Data_science](#data_science)
* [Java](#java)

---

### Md

- [Tips for Formatting MD](MD/formatting_markdown.md)

### Data_science

- [# Maturação de Dados](data_science/maturação_de_dados.md)
- [# Overfitting](data_science/overfit.md)
- [MatPlotLib: Scatter Plot](data_science/mlp_scatter_plot.md)

### Java

- [# Java Abstract Classes and Methods](java/abstract.md)

## Usage

After creating a new entry, run `./createReadme.py > README.md` to regenerate
the readme with the new data.

If you are using git, you can install this script as a pre-commit git hook so
that it is autogenerated on each commit.  Use the following command:
    cd .git/hooks/ && ln -s ../../createReadme.py pre-commit && cd -


## About

I shamelessly stole this idea from
[jbranchaud/til](https://github.com/jbranchaud/til) who claims to have stolen
it from others.

## Other TIL Collections

* [jbranchaud/til](https://github.com/jbranchaud/til) who claims to have stolen
* [jima80525/til](https://github.com/jima80525/til)
* [Today I Learned by Hashrocket](https://til.hashrocket.com)
* [jwworth/til](https://github.com/jwworth/til)
* [thoughtbot/til](https://github.com/thoughtbot/til)

## License

&copy; 2020 Lucas Pimenta

This repository is licensed under the MIT license. See `LICENSE` for
details.