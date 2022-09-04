# Changelog

## sphinx-autoissues v0.0.2 (unreleased)

### Development

- Add [flake8-bugbear](https://github.com/PyCQA/flake8-bugbear) (#3)

## sphinx-autoissues v0.0.1 (2022-08-27)

### Resolution disabled by default

- New option: `issuetracker_resolve_issues`

  Default `False`. Set to `True` to re-enable.

- When a URL isn't resolved, the URL will fall back to `issuetracker_url_template`

### Docs to Markdown (#2)

Documentation

- moved from reStructuredText to markdown
- Use furo theme

### Overhaul (#1)

Packaging:

- Rename `sphinxcontrib-issuetracker` to `sphinx_autoissues`
- build: Add pyproject.toml (Poetry)

Documentation:

- docs: `doc/` -> `docs/`

Trackers:

- Remove all trackers except Github

Typing:

- Add type annotations (`mypy --strict` compatible)
- `sphinx_autoissues.types`

Meta:

- isort, black, flake8 configuration
- Run through black and isort
- Deprecate python 2.7 code via pyupgrade

  ```sh
  pip install pyupgrade autoflake; \
  pyupgrade --py37 tests/**/*.py docs/**/*.py sphinx_autoissues/**/*.py; \
  poetry run autoflake tests/**/*.py docs/**/*.py sphinx_autoissues/**/*.py -i --ignore-init-module-imports; \
  make black isort
  ```

Tests:

- Remove travis
- Add github workflow
- Migrate from `pytest_funccarg__` to `pytest.fixture` (see
  [pytest 2.3 docs](https://docs.pytest.org/en/7.0.x/funcarg_compare.html#shortcomings-of-the-previous-pytest-funcarg-mechanism))
- Remove old tests and start from scratch - I gave this 3 nights and my rationale is:
  1. I am not familiar with old style pytest, and
  2. I can't read pytest custom marks or test generations (see reason 6)
  3. A lot of the old demo fixtures are pointing to issues and services e.g.
     https://bitbucket.org/birkenfeld/sphinx that don't exist
  4. My real use case is just GitHub
  5. There's `sphinx.testing.fixtures` now
  6. I prefer `pytest.mark.parametrize`

Sphinx updates:

- See [Sphinx docs on deprecated APIs](https://www.sphinx-doc.org/en/master/extdev/deprecated.html)

## Earlier

### From sphinxcontrib-issuetracker

#### sphinxcontrib-issuetracker 0.11 (Jan 17, 2013)

- Send proper user agent in API requests
- #4: Respect Github rate limits
- #5: Fix compatibility with requests 1.0

#### sphinxcontrib-issuetracker 0.10.1 (Jun 19, 2012)

- Fix README rendering on PyPI
- #1: Fix test failure on Python 3

#### sphinxcontrib-issuetracker 0.10 (Jun 18, 2012)

- Extension now hosted at <https://github.com/lunaryorn/sphinxcontrib-issuetracker>
- Use requests library for HTTP requests
- Consider launchpad issues closed only if all referenced tasks are completed
- Support Python 3 (with exception of `launchpad` and `debianbts` trackers)

#### sphinxcontrib-issuetracker 0.9 (Aug 31, 2011)

##### Incompatible changes

- Remove {confval}`issuetracker_expandtitle`, use `issuetracker_title_template = '{issue.title}'`
  instead
- Rename `issuetracker-resolve-issue` to {ref}`issuetracker-lookup-issue`

##### Other changes

- New features:

  - Add {rst:role}`issue` role for explicit issue references
  - Add {confval}`issuetracker_title_template`
  - Add {confval}`issuetracker_plaintext_issues`
  - Use issue title as link title

- Bug fixes and improvements:

  - Fix TypeError caused by `launchpad` issue tracker
  - Fix issue title in `launchpad` issue tracker
  - Fix detection of closed issues in `launchpad` issue tracker
  - Fix CSS classes for issue references to be more compatible with Sphinx themes

#### sphinxcontrib-issuetracker 0.8 (Aug 24, 2011)

##### Incompatible changes

- Require Python 2.6 or newer now
- Remove `issuetracker_user` configuration value, GitHub and BitBucket projects must include the
  username now
- Custom resolvers must return {class}`~sphinxcontrib.issuetracker.Issue` objects instead of
  dictionaries now
- Change signature of `issuetracker-resolve-issue`

##### Other changes

- General:

  - Builtin `debian` tracker is fully supported now

- New features:

  - Add [Jira] support
  - Add {confval}`issuetracker_url`
  - Add {confval}`issuetracker_expandtitle`

- Bugs fixes and improvements:

  - Use BitBucket API instead of scraping the BitBucket website
  - Cache failed issue lookups, too

#### sphinxcontrib-issuetracker 0.7.2 (Mar 10, 2011)

- Fix source distribution to include tests again
- Fix extraction of issue state for open issues from bitbucket
- Ignore references in inline literals and literal blocks

#### sphinxcontrib-issuetracker 0.7.1 (Jan 19, 2011)

- Copy the stylesheet after build again to avoid exceptions on non-existing build directories

#### sphinxcontrib-issuetracker 0.7 (Jan 08, 2011)

- Issue information is now cached
- Custom issue trackers must now connect to the `issuetracker-resolve-issue` event, the builtin
  `missing-reference` event is no longer used.

#### sphinxcontrib-issuetracker 0.6 (Jan 04, 2011)

- Add support for the debian bugtracker (thanks to Fladischer Michael)
- Fix NameError in launchpad issue tracker
- Use HTTPS for BitBucket

#### sphinxcontrib-issuetracker 0.5.4 (Nov 15, 2010)

- Use HTTPS for Github

#### sphinxcontrib-issuetracker 0.5.3 (Nov 14, 2010)

- Add license text to source tarball

#### sphinxcontrib-issuetracker 0.5.2 (Sep 17, 2010)

- Issue reference resolvers get the application object now as fourth argument. The environment is
  availabe in the `.env` attribute of this object.
- Fix the URL of Google Code issues (thanks to Denis Bilenko)
- Fix detection of closed issues in Google Code (thanks to Denis Bilenko)
- Improve error message, if `issuetracker_issue_pattern` has too many groups (thanks to Denis
  Bilenko)
- Add warnings for unexpected HTTP status codes in BitBucket and Google Code issue trackers

#### sphinxcontrib-issuetracker 0.5.1 (Jul 25, 2010)

- Fix client string for launchpad access

#### sphinxcontrib-issuetracker 0.5 (Jul 21, 2010)

- Closed issues are automatically struck trough in HTML output
- Require Sphinx 1.0 now
- Fix installation on Windows

#### sphinxcontrib-issuetracker 0.4 (May 21, 2010)

- Misc spelling fixes

#### sphinxcontrib-issuetracker 0.3 (May 02, 2010)

- Add support for Google Code
- Add support for Launchpad
- Issue tracker callbacks get the build environment now

#### sphinxcontrib-issuetracker 0.2 (Apr 13, 2010)

- Use `missing-reference` event instead of custom event

#### sphinxcontrib-issuetracker 0.1 (Apr 10, 2010)

- Initial release

[jira]: http://www.atlassian.com/software/jira/

<!---
vim: set filetype=markdown:
-->
