This folder contains scripts that help with the development and release of natu.

The [pre-commit script](pre-commit) prevents commits if there are errors in the
Python source or there are filenames with non-ASCII characters.  It also adds
an "UNRELEASED" markdown file in the base folder if there is no version marked
in [natu/__init__.py](../natu/__init__.py).

The [post-checkout script](post-checkout) removes byte-compiled Python files
(*.pyc) when switching branches.  Since the source may change when upon
checkout, the *.pyc files should be recompiled to prevent confusion.

Other scripts ([code.sh](code.sh), [doc.sh](doc.sh), etc.) are linked to [git]
via aliases.

#### Installation

Copy [pre-commit](pre-commit) and [post-checkout](post-checkout) to
*.git/hooks/*.

Add to *.git/config*:

    [alias]
        cloc = !bash `git rev-parse --show-toplevel`/hooks/cloc.sh
	    diff-ini = !bash `git rev-parse --show-toplevel`/hooks/diff-ini.sh
        pylint = !bash `git rev-parse --show-toplevel`/hooks/pylint.sh
	    doc = !bash `git rev-parse --show-toplevel`/hooks/doc.sh
	    code = !bash `git rev-parse --show-toplevel`/hooks/code.sh

#### Usage

##### For source code:

To clean/remove the built code (alias for `setup.py clean --all`):

    git code clean

To build/make a distributable copy and run tests:

    git code build

To release/upload a version to [PyPI]\:

    git code release

##### For documentation:

To clean/remove the built documentation:

    git doc clean

To build/make the HTML documentation, with an option to rebuild the static
images and spellcheck the pages:

    git doc build

To release/publish the documentation to the [GitHub webpage]\:

    git doc release

##### Other:

To compare the \*.ini files to their ReST tables in the documentation:

    git diff-ini

To run [pylint](http://www.pylint.org/) on all of the source files:

    git pylint

To count the number of lines of code:

    git cloc

#### Development workflow

All releases and updates are on the `master` branch.  During the build process,
(`git code build`), releases are tagged  as "v*major*.*minor*.*micro*", where
*major*, *minor*, and *micro* are the integer parts of the version number.  The
unreleased updates have an "UNRELEASED.md" file in the base folder with the
commit date/time and the author.

The version number is recorded in [natu/__init__.py](../natu/__init__.py).  It
is *None* for unreleased copies.  When the documentation is built
(`git doc build`), the download link and text is updated with information from
the last tag, which corresponds to the last release.


[git]: http://git-scm.com/
[GitHub webpage]: kdavies4.github.io/natu/
[PyPI]: https://pypi.python.org/pypi/natu
