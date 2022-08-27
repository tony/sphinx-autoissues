# Configuration

## General configuration

Add `sphinx_autoissues` to the configuration value {confval}`extensions` to enable this extensions
and configure the extension:

```{confval} issuetracker

The issuetracker to use.  As of now, the following trackers are
supported:

- `github`: The issue tracker of https://github.com.
```

````{confval} issuetracker_project

The project inside the issue tracker or the project, to which the issue
tracker belongs.  Defaults to the value of :confval:`project`.


```{note}
  In case of BitBucket and GitHub, the project name must include the name
  of the user or organization, the project belongs to.  For instance, the
  project name of Sphinx_ itself is not just `sphinx`, but
  `birkenfeld/sphinx` instead.  If the user name is missing, a
  :exc:`~exceptions.ValueError` will be raised when an issue is to be
  resolved the first time.
```

````

```{confval} issuetracker_url

The base url of the issue tracker::

  issuetracker = 'jira'
  issuetracker_url = 'https://studio.atlassian.com'

Required by all issue trackers which do not only have a single instance, but
many different instances on many different sites.

```

```{confval} issuetracker_redmine_key

The API Key that is set on the Redmine server accounts page. If
authentication failed, an error will be thrown and the build will fail.
```

```{confval} issuetracker_redmine_username

You usually don't need this to be set if you are using the API key, but if
you do use this, do set the password configuration value as well.
```

```{confval} issuetracker_redmine_password

Works together with :confval:`issuetracker_redmine_username`.
```

```{confval} issuetracker_redmine_requests

`python-redmine` heavily uses the `requests` module for all its
communications with the redmine server. If you do need to send some values
down to the Requests module, you need to configure this with a dict. By
default, this is an empty dict. An useful usecase for this parameter is to
set the `verify` value to `False` so as to disable certificate
verification on SSL requests on self signed server, for example.
```

## Plaintext issues

```{confval} issuetracker_plaintext_issues

If `True` (the default) issue references are extracted from plain text by
turning issue ids like `#10` into references to the corresponding issue.
Issue ids in any kind of literal text (e.g. `inline literals` or code
blocks) are ignored.  If `False`, no issue references are created from
plain text.

Independently of this configuration value, you can always reference issues
explicitly with the :rst:role:`issue` role.
```

By default the extension looks for issue references starting with a single dash, like `#10`. You can
however change the pattern, which is used to find issue references:

```{confval} issuetracker_issue_pattern

A regular expression, which is used to find and parse issue references.
Defaults to `r'#(\d+)'`.  If changed to `r'gh-(\d+)'` for instance,
this extension would not longer recognize references like `#10`, but
instead parse references like `gh-10`.  The pattern must contain only a
single group, which matches the issue id.
```

Normally the reference title will be the whole issue id. However you can also use a custom reference
title:

```{confval} issuetracker_title_template

A `format string`_ template for the title of references created from
plaintext issue ids.  The format string gets the :class:`Issue` object
corresponding to the referenced issue in the `issue` key, you may use any
attributes of this object in your format string.  You can for instance
include the issue title and the issue id::

  issuetracker_title_template = '{issue.title} ({issue.id})'

If unset, the whole text matched by :confval:`issuetracker_issue_pattern` is
used as reference title.
```

[debianbts]: http://pypi.python.org/pypi/python-debianbts/
[format string]: http://docs.python.org/library/string.html#format-string-syntax
[jira]: http://www.atlassian.com/software/jira/
[launchpadlib]: http://pypi.python.org/pypi/launchpadlib/
[soappy]: http://pypi.python.org/pypi/SOAPpy/
[sphinx]: http://sphinx.pocoo.org
[sphinx issue tracker]: https://bitbucket.org/birkenfeld/sphinx/issues/
