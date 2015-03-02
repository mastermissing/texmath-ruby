# texmath-ruby

[![Build Status](https://img.shields.io/travis/hollingberry/texmath-ruby.svg)](https://travis-ci.org/hollingberry/texmath-ruby)
[![Gem Version](https://img.shields.io/gem/v/texmath-ruby.svg)](https://rubygems.org/gems/texmath-ruby)
[![Gem Downloads](https://img.shields.io/gem/dt/texmath-ruby.svg)](https://rubygems.org/gems/texmath-ruby)
[![Code Climate](https://img.shields.io/codeclimate/github/kabisaict/flow.svg)](http://codeclimate.com/github/hollingberry/texmath-ruby)

A wrapper for [TeXMath](https://github.com/jgm/texmath), a Haskell library for
converting between formats used to represent mathematics.

TeXMath can convert between LaTeX, presentation MathML, and OMML (Office Math
Markup Language). This wrapper uses the command line program for
texmath for all operations (rather than interface directly with the
Haskell library) and is heavily based on
[William Melody's wrapper](https://github.com/alphabetum/pandoc-ruby)
for [Pandoc](https://github.com/jgm/pandoc).

## Installation

First, make sure [texmath](https://github.com/jgm/texmath) is installed. If you
already have [The Haskell Platform](https://www.haskell.org/platform/), you can
install texmath with Cabal:

```shell
$ cabal install texmath
```

If you use [Bundler](http://bundler.io), then add this line to your
application's Gemfile:

```ruby
gem 'texmath-ruby', require: 'texmath'
```

And then execute:

```shell
$ bundle
```

Or install it yourself as:

```shell
$ gem install texmath-ruby
```

## Usage

Once everything is installed correctly, using TeXMath is incredibly easy.

For example, converting from LaTeX to MathML looks like this:

```ruby
TeXMath.convert('\sqrt{x^3}', from: :tex, to: :mathml)
  # => '<math display="block" xmlns=...'
```

TeXMath can convert between LaTeX, MathML, and OMML, in any
direction. By default (if either the source or destination format
isn't explicitly specified), TeXMath will try to convert from LaTeX to
MathML. So to convert from LaTeX, the default source format, to OMML:

```ruby
TeXMath.convert('\sqrt{x^3}', to: :omml)
  # => '<m:oMathPara>...'
```

Or from OMML to MathML, the default destination format:

```ruby
TeXMath.convert('<m:oMathPara>...', from: :omml)
  # => '<math display="block" xmlns=...'
```

TeXMath also comes with writers for XHTML and Pandoc's native format.

## Supported formats

|             Format            |    Symbol    |  Reader  |  Writer  |
|-------------------------------|--------------|----------|----------|
| LaTeX                         | `:tex`       | &#10004; | &#10004; |
| MathML                        | `:mathml`    | &#10004; | &#10004; |
| Office Math Markup Language   | `:omml`      | &#10004; | &#10004; |
| TeXMath native                | `:native`    | &#10004; | &#10004; |
| XHTML                         | `:xhtml`     |          | &#10004; |
| Pandoc native                 | `:pandoc`    |          | &#10004; |

## Contributing

1. Fork it ( https://github.com/hollingberry/texmath-ruby/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
