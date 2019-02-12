The First Line Must Be the Blog Title
![](https://jfrog.info/wp-content/uploads/2019/01/863X300.jpg)
Added the header image
Here is another change to test the auto update feature.
This is my change. 
The English actor Christopher Bullock [said](https://www.mightytaxes.com/death-taxes-quote-history/) that “Tis impossible to be sure of anything but Death and Taxes.” While he certainly wasn’t a software developer, I think that, if he was, the quote would have definitely included the use of software dependencies.

Developers usually make use of other packages, modules, libraries, or whatever your favorite programming language might call it, to make their lives easier. They don’t have to reinvent the wheel and can benefit from the knowledge of other developers. Those packages need to be stored somewhere, to prevent [disappearing code](https://www.theregister.co.uk/2016/03/23/npm_left_pad_chaos/) breaking your builds and to make sure your team has access to the same versions.

> I want to have reproducible builds on different computers at different times. This is currently problematic; let’s make things better. — [David Hinkes](https://plus.google.com/+DavidHinkes/posts/gczN5SQ94ek)

## Getting the right things

The `go get` command, up to version 1.11, doesn’t have any arguments to specify which version of a specific import was needed. That lead to a rise in build and management tools, like [gb](https://getgb.io/) and later [dep](https://golang.github.io/dep/), trying to solve that problem. They did indeed solve the problem of having a set version of a package available, but those packages were stored in a “vendor” folder and that folder usually ended up in a version control system. Why is that “vendoring” isn’t such a great thing?

The obvious downside is that because you store the dependencies in your repositories they’ll be, as a whole, bigger and potentially even a lot bigger. That also means any git operation will take a longer time to complete, including the builds you need to push to production to fix that one critical bug.

Storing the version you depend on makes for a more reproducible build, as you’re safeguarded from updates to the master branch of that dependency ([or worse](https://www.theregister.co.uk/2016/03/23/npm_left_pad_chaos/)…), but it remains a poor man’s version of source control. It also means your PRs will list all changes in the vendor tree and it’s close to impossible to work with multiple versions of the same dependency.

> Versioning is a source of significant complexity, especially in large code bases, and it has taken some time to develop an approach that works well at scale in a large enough variety of situations to be appropriate to supply to all Go users. — [Go FAQ on versions](https://golang.org/doc/faq#get_version)

## So now what?

The release of [Go 1.11](https://golang.org/doc/go1.11#modules) didn’t only introduce the ability to develop code outside of your GOPATH, but also introduced the concept of modules with integrated support for versioning and package distribution.

> Using modules, developers are no longer confined to working inside GOPATH, version dependency information is explicit yet lightweight, and builds are more reliable and reproducible. — [Go Release Notes](https://golang.org/doc/go1.11#modules)

The introduction of modules in Go was likely one of the most debated and anxiously awaited features as it gives developers the control they’ve been looking for. Modules provide:

* Versioning: Each git tag and even each git commit can be seen as a separate version that can be used;
* Reproducibility: Each app that makes use of Go modules has two files that describe what the exact dependencies are making it reproducible on different computers at different times;
* Maintainability: Each developer in the team knows exactly which versions are used and PRs will list changes in the dependencies;
* Cleaner repositories: Developers no longer have to check in the vendor tree, leading to smaller repositories.

## What about immutability?

Good that you’re still here! Immutability is the only thing I haven’t really touched on but is really important for reproducible builds and as we move away from vendoring that need doesn’t change. Immutability, and the assurance other developers have access to the same versions, is provided by tools like [Project Athens](https://github.com/gomods/athens) and [JFrog Artifactory](https://jfrog.com/artifactory/) (for in-house use) and [JFrog GoCenter](https://jfrog.com/gocenter/) for public use!

## What’s next?

While tools like [dep](https://github.com/golang/dep) will likely be around for some time, the Go community is actively working towards the adoption of Go modules and making that more robust in the upcoming releases. If you haven’t done so already, this would be a good time to check out some tutorials [here](https://roberto.selbach.ca/intro-to-go-modules/) and [here](https://ukiahsmith.com/blog/a-gentle-introduction-to-golang-modules/) and check out [GoCenter](https://jfrog.com/gocenter/)!
