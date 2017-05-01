+++
date = "2017-04-30T21:19:59-05:00"
draft = true
title = "Golang and the Next-Gen Build Tools"

+++

The three general build systems from the big players. Bazel by Google, Pants by Twitter and Buck by Facebook, all attempt to allay the problems plaguing build system since time immemorial. They are all based on the internal build system from Google, Blaze, and as such, they are almost identical in features. They improve on the correctness, speed and modularity of the builds with features such as sandboxed builds, caching of targets, and namespacing of build modules. 

They enforce the correctness of the task definitions and its dependencies, and thereby allow the optimization of incremental builds by caching intermediate results. They have client-server implementations to allow significant speedup of build operations. They are extensible and configurable. 

So, how do they compare? Which one is best? Well, for starters, here’s a table of features:


| Build Tool    | Ease of Installation        | Windows Support | Go Support | Other |
|---------------|-----------------------------|-----------------|------------|-------|
| Bazel         | Single script installer     | Beta            |  <ul style="list-style:none;padding-left:0"><li>Beta:</li><li>- Rudimentary dependency management<li>- Bootstraps `go` tool</li><li>- Cgo</li></ul> | <ul style="padding-left:1rem"><li>iOS, Android</li><li>C++, Java, Python</li><li>Rust</li><li>Javascript using Closure (3rd party support for NodeJS)</li><li>Docker</li> |
| Pants         | Check-in-able runner script | Nope            | <ul style="list-style:none;padding-left:0"><li>Good:</li><li>- Good-ish dependency management</li><li>- go-fmt (beta)</li><li>- Bootstraps `go` tool</li></ul> |<ul style="padding-left:1rem"><li>iOS, Android</li><li>C++, Java, Python</li><li>Javascript through NodeJS</li><li>Rust</li></ul>|
| Buck          | <ul style="list-style:none;padding-left:0"><li>Mac</li><li>- Brew tap</li><li>Linux/Windows</li><li>- Build from source</li></ul>| Yes | <ul style="list-style:none;padding-left:0"><li>Basic:</li><li>- No bootstrapping of `go` binary.</li><li>- No dependency management.</li></ul> |  <ul style="padding-left:1rem"><li>iOS, Android</li><li>C++, Java, Python</li><li>Haskell</li><li>Rust</li></ul> |

Pants is the first of the three to be released as open source, and it shows, it is the one with the shiniest features. It has good dependency management, integration with the tools you're probably using now and it is easy to setup whether it is on your workstation or remote build machines.

Next up is Bazel. It feels like an industrial grade tool, with a nice web page, lots of stars on its github page and Windows support. But it is still lagging in features compared to pants. The lack of good dependency management means you will be writing dependency files by hand. No support for coverage means you'll have to run scripts on the side. The goals of the Bazel project are more geared towards big companies and not for small projects (which is to be expected of Google). Depending on what language your project is mainly written (say Python[^1]) Bazel might not be ready for prime time, unless you're already vendoring (copying) 3rd party code into your repository or if you're willing to make the (non-trivial) change.


As for Buck, well, it is a tool more geared towards front-end and mobile development. And it looks like a really good tool if you work on that segment. But you'll need to build it yourself if you want to use it on Linux, and that's a show stopper for me (at least give me bootsrap script!). Really nice output and good support for Windows might make this your first choice. Do note that Buck is the youngest of the tools, perhaps it will take over the build system world?

## Summary

If limiting our scope to projects using Go, Pants takes the cake. It's [documentation](https://pantsbuild.github.io/go_readme.html) for Go is top notch, and it walks you through the whole process. They're pretty responsive on their [community](https://groups.google.com/forum/#!forum/pants-devel) channels, specially on [slack](https://pantsslack.herokuapp.com/). Trying up and coming features is as simple as changing the Pants version in the `pants.ini` file. And if you extend your considerations to other languages, you'd be more than satisfied with Python+Pip+PEX support, NodeJS+NPM, along with the usual C++ and Java.

Perhaps the best build tool will not remain the same one. Let's hope that the open source model shared by the tools will enhance their improvement through the competition and sharing of features. But, whether it is Pants, Buck or Bazel, these Next-Gen build tools feel like the future even if you're not following the monorepo structure in your organization. I keep wondering where the hype behind the next-gen build tools is, I would consider starting to use these tools, if only for the speedups in builds[^2]. Now, if you add build correctness and code organization improvements to the mix...

What do you think?

[^1]: [Bazel vs. Pants for a Python project](http://tanin.nanakorn.com/blogs/371)
[^2]: [Buck - life is too short to spend a minute for each build](http://zserge.com/blog/buck-build-system.html)
