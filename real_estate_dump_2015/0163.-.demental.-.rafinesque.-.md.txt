# rafinesque
Customize your application semantics.

[![Code Climate](https://codeclimate.com/github/demental/rafinesque/badges/gpa.svg)](https://codeclimate.com/github/demental/rafinesque)
[![Build Status](https://travis-ci.org/demental/rafinesque.svg)](https://travis-ci.org/demental/rafinesque)
[![Dependency Status](https://gemnasium.com/demental/rafinesque.svg)](https://gemnasium.com/demental/rafinesque)
[![Test Coverage](https://codeclimate.com/github/demental/rafinesque/badges/coverage.svg)](https://codeclimate.com/github/demental/rafinesque)

## What is it ?
You have created an Ruby application, which functional specifications can be applied to various domains.

*Problem* : the texts in your app are somewhat tied to a specific domain, unless you add many placeholders to your translations yml files, and, more problematic, inject values to these placeholders everywhere in your views, mailers ... and so on...

### Example
Let's say you have a classified app, specialized in real estate. Your application.en.yml file looks like this:

```yml
en:
  home:
    title: Real estate classified
  search:
    title: Find a home for sale.

```

Now you want to fork your project and create a classified to sell yachts. Therefore you have to update your translations :

```yml
en:
  home:
    title: Marine classified
  search:
    title: Find a boat for sale.

```

You will now have issues maintaining this fork, because it's a fork. So you decide to put placeholders and inject variables in your views:


```yml
en:
  home:
    title: %{domain_capitalized} classified
  search:
    title: Find a %{sold_object} for sale.

```

Then in your views :

```haml
 = t('.title', domain_capitalized: some_var)
```

And your views start to get bloated...

*Solution*

Here comes Rafinesque. Rafinesque allows you to make custom, localized placeholders inside your translated strings, that are substituted when translations are loaded in memory.

*Setup*

1. Add Rafinesque to your Gemfile

```ruby
  gem "rafinesque"
```

2. Install rafinesque
* On rails projects, run ```rails generate rafinesque:install```
* on non-Rails, include the rafinesque module somewhere in your bootstrap sequence :

```ruby

require 'rafinesque/i18n_backend'
I18n::Backend::Simple.include(Rafinesque::I18nBackend)

```

3. Add your semantics in a json string, in ENV (you may use Figaro for example, to load a yaml into ENV)

```ruby
  ENV['semantics']= "{\"fr\":{\"Real estate\":\"Marine\",\"home\":\"yacht\",\"maison\":\"bateau\"", \"fr\":{\"l'immobilier\":\"la marine\",\"maison\":\"bateau\""
```

4. Insert some placeholders in your yml translations files (must be surrounded with $). The important thing to understand is that these placeholders are not variables, they are some real words. This allows you to make sure that you handle all the syntactical odds and ends of your language :

```yml
en:
  home:
    title: The best $Real estate$ listing website
  search:
    title: Find a $home$ for sale
```

### Roadmap

* Be smarter about variants (e.g. automatically handle titleized versions)
* Add more test (test and extract the currently private recursive_map method).
* Add more storage systems than ENV (database or yml files for example).
* Allow to customize placeholders syntax.
* Create rake tasks to extract existing placeholders.
* Make sure it can be used with other I18n backend than the default one (I18n::Backend::Simple).

