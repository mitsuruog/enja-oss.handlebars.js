**Using the Handlebars precompiler, you can precompile your Handlebars templates to save time on the client and reduce the required runtime size of the handlebars library.**

## Getting Started

First, you will need to install node and npm. On OSX:

```
$ brew install node
$ curl https://npmjs.org/install.sh | sh
```

This assumes you already have Homebrew installed. If not, install it first.

```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
```

Next, install the Handlebars npm package.

```
$ npm install handlebars -g
```

Using the `-g` flag installs the package globally, so it can be used in any project.

Now, you're ready to use the precompiler:

```
$ handlebars <input> -f <output>
```

The compiler will insert templates in `Handlebars.templates`. If your input file is `person.handlebars`, the compiler will insert it at `Handlebars.templates.person`.

If you're working with precompiled templates, you don't need to ship the compiler with your deployed application. Instead, you can use the smaller "runtime" build.

```
<script src="/libs/handlebars.runtime.js"></script>
```

In addition to reducing the download size, eliminating client-side compilation will significantly speed up boot time, as compilation is the most expensive part of Handlebars.

## Optimizations

Because you are precompiling templates, you can also apply several optimization to the compiler. The first allows you to specify a list of the known helpers to the compiler

```
handlebars <input> -f <output> -k each -k if -k unless
```

The Handlebars compiler will optimize accesses to those helpers for performance.