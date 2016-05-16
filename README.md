# Test Smells

This repository is designed to serve as a sandbox for exploring a handful of test
smells that are common in real-world test suites.

## Getting started

First, clone the repo, change into its directory, and make sure your
[Node.js](http://nodejs.org) environment is working okay:

```
$ npm install
$ npm test
```

The tests should pass. (If a few tests fail, that's okay. Some of the tests are
designed to fail erratically.)

## Working through the repo

Each of our odorous tests are organized under the `smells/` directory and broken
down into categories.

### The tests

Each smell's file listing is structured the same way, starting with:

#### The description

Each file starts with a comment which contains:

* A simple description of the smell
* An enumeration of the problems the smell might indicate
* For each potential problem, a general prescribed approach for refactoring the
test (or the test's subject) to eliminate the smell

Remember, not every smell you detect in the wild indicates an actual problem!
Smells are simply surface indications of common problems and not necessarily
problematic in-and-of-themselves.

#### The subject under test

After the comment will be one to several functions meant to be the "production"
source code. Typically these would be broken out into a separate file, but to
keep everything straightforward, each smell is kept to a single file listing.

For the purpose of keeping the examples easy-to-understand, the subject code is
typically minimal and trivial, unless greater complexity is called for by the
test smell itself.

#### The smelly test

This repo's tests are written for our
[teenytest](https://github.com/testdouble/teenytest) module, which means that
the value of `module.exports` is considered to be "the test" by the test runner.
If `module.exports` is set to a function, then that's the only test in the file
listing. If a plain object is assigned to `module.exports`, however, then each
function on the object is considered its own test. It may be the case that only
one of the tests exported by a file exhibit the smell in the description, or that
multiple tests could stand to be reworked.

### Working with the tests

#### Improve the test

Once you've read the description of the test smell, try to sniff it out among the
file listing's tests.

From there, attempt to identify which root cause in the description is causing
the smell to emanate and attempt to implement its prescription for reworking
the test. (In a few cases, a test's improvements will depend on refactoring the
subject code as well.)

Remember, the tests themselves are untested, so be sure that your
new-and-improved test still works! Consider forcing the test to break with a
message that indicates it's working as expected before you commit your changes.
We like to say, "never trust a test you haven't seen fail," for this reason.

#### Compare with our solution

We'll maintain a git branch named `solutions` which will tidy up the tests to our
own likely. If you're interested in seeing our approach to deodorizing a
particular issue, stash or commit your own changes and `git checkout solutions`
to take a peek, before switching back to your branch with `git checkout -`.

If your solution doesn't look like ours, don't lose heart! There's more than one
way to write a good test. So long as you've resolved the smell and you feel like
your changes communicate the intent well, you've probably left things in a better
state than you found them in.
