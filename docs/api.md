# API

```{eval-rst}
.. module:: sphinx_autoissues
   :synopsis: Parse issue references and link to the corresponding issues
```

To use an issue tracker not supported by this extension, set {confval}`issuetracker` to `None` or
leave it unset, and connect your own callback to the event {ref}`issuetracker-lookup-issue`:

(issuetracker-lookup-issue)=

## Events

```{eval-rst}
.. confval:: issuetracker-lookup-issue(app, tracker_config, issue_id)

   Emitted if the issue with the given ``issue_id`` should be looked up in the
   issue tracker.  Issue tracker configured is provided by ``tracker_config``.

   ``app`` is the Sphinx application object.  ``tracker_config`` is the
   issuetracker configuration as :class:`TrackerConfig` object.  ``issue_id``
   is the issue id as string.

   A callback should return an :class:`Issue` object containing the looked up
   issue, or ``None`` if it could not find the issue.  In the latter case other
   callbacks connected to this event are be invoked by Sphinx.
```

Refer to the [builtin trackers] for examples.

## Structures

```{eval-rst}
.. autoclass:: TrackerConfig

   .. attribute:: project

      The project name as string.

   .. attribute:: url

      The url of the issue tracker as string *without* any trailing slash, or
      ``None``, if there is no url configured for this tracker.  See
      :confval:`issuetracker_url`.
```

```{eval-rst}
.. autoclass:: Issue

   A :class:`~typing.NamedTuple` providing issue information.

   .. attribute:: id

      The issue id as string.

      If you are writing your own custom callback for
      :ref:`issuetracker-lookup-issue`, set this attribute to the
      ``issue_id`` that was given as argument.

   .. attribute:: title

      The human readable title of this issue as string.

   .. attribute:: url

      A string containing an URL for this issue.

      This URL is used as hyperlink target in the generated documentation.
      Thus it should point to a webpage or something similar that provides
      human-readable information about an issue.

   .. attribute:: closed

      ``True``, if the issue is closed, ``False`` otherwise.
```

[builtin trackers]:
  https://github.com/tony/sphinx-autoissues/blob/master/sphinx_autoissues/resolvers.py
