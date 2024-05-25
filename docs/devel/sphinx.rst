{"uuid": "49ed550a-b30f-11eb-ab45-00155d9a47a8", "device_id": "android-49ed5762b30f11eb", "ad_id": "00ea607f-90b5-01af-95ac-c6f37ac93fbd", "session_id": "49ed5848-b30f-11eb-ab45-00155d9a47a8", "cookie": {"__class__": "bytes", "__value__": "gASVRwMAAAAAAAB9lIwOLmluc3RhZ3JhbS5jb22UfZSMAS+UfZQojAljc3JmdG9rZW6UjA5odHRw\nLmNvb2tpZWphcpSMBkNvb2tpZZSTlCmBlH2UKIwHdmVyc2lvbpRLAIwEbmFtZZSMCWNzcmZ0b2tl\nbpSMBXZhbHVllIwgemxlTm5zWjBJeUFPa0NPTzkwVG5rOUc0RHJDbFIzcHCUjARwb3J0lE6MDnBv\ncnRfc3BlY2lmaWVklImMBmRvbWFpbpSMDi5pbnN0YWdyYW0uY29tlIwQZG9tYWluX3NwZWNpZmll\nZJSIjBJkb21haW5faW5pdGlhbF9kb3SUiIwEcGF0aJRoA4wOcGF0aF9zcGVjaWZpZWSUiIwGc2Vj\ndXJllIiMB2V4cGlyZXOUSgCUe2KMB2Rpc2NhcmSUiYwHY29tbWVudJROjAtjb21tZW50X3VybJRO\njAdyZmMyMTA5lImMBV9yZXN0lH2UdWKMA21pZJRoCCmBlH2UKGgLSwBoDGggaA6MHFlKdXhfUUFC\nQUFHUmtGeFRzblNuek5DakpCdXCUaBBOaBGJaBKMDi5pbnN0YWdyYW0uY29tlGgUiGgViGgWaANo\nF4hoGIhoGUr9GF5kaBqJaBtOaBxOaB2JaB59lHVijANydXKUaAgpgZR9lChoC0sAaAxoJmgOjANO\nQU+UaBBOaBGJaBKMDi5pbnN0YWdyYW0uY29tlGgUiGgViGgWaANoF4hoGIhoGU5oGohoG05oHE5o\nHYloHn2UjAhIdHRwT25seZROc3VijApkc191c2VyX2lklGgIKYGUfZQoaAtLAGgMaC1oDowLNDc2\nNTU2NjY1MjeUaBBOaBGJaBKMDi5pbnN0YWdyYW0uY29tlGgUiGgViGgWaANoF4hoGIhoGUoAWRJh\naBqJaBtOaBxOaB2JaB59lHVijAlzZXNzaW9uaWSUaAgpgZR9lChoC0sAaAxoM2gOjCA0NzY1NTY2\nNjUyNyUzQUFkSjZxZkhDZGt2SHdpJTNBM5RoEE5oEYloEowOLmluc3RhZ3JhbS5jb22UaBSIaBWI\naBZoA2gXiGgYiGgZSoDlfGJoGoloG05oHE5oHYloHn2UjAhIdHRwT25seZROc3VidXNzLg==\n"}, "created_ts": 1620816384}

--------------------------------------

`Sphinx`_ is a tool for creating beautiful documentation. It uses simple
reStructuredText syntax and can generate output in many formats. If you're
looking for an example, this documentation is also built using it. The very
useful companion for using Sphinx is the `Read the Docs`_ service, which will
build and publish your documentation for free.

I will not focus on writing documentation itself, if you need guidance with
that, just follow instructions on the `Sphinx`_ website. Once you have
documentation ready, translating it is quite easy as Sphinx comes with support
for this and it is quite nicely covered in their :ref:`sphinx:intl`.  It's
matter of few configuration directives and invoking of the ``sphinx-intl``
tool.

If you are using Read the Docs service, you can start building translated
documentation on the Read the Docs. Their :doc:`rtd:localization` covers pretty
much everything you need - creating another project, set its language and link
it from main project as a translation.

Now all you need is translating the documentation content. Sphinx generates PO
file for each directory or top level file, what can lead to quite a lot of
files to translate (depending on :confval:`sphinx:gettext_compact` settings).
You can import the :file:`index.po` into Weblate as an initial component and
then configure :ref:`addon-weblate.discovery.discovery` add-on to automatically
discover all others.


.. list-table:: Component configuration

   * - :ref:`component-name`
     - ``Documentation``
   * - :ref:`component-filemask`
     - ``docs/locales/*/LC_MESSAGES/index.po``
   * - :ref:`component-new_base`
     - ``docs/locales/index.pot``
   * - :ref:`component-file_format`
     - `gettext PO file`
   * - :ref:`component-check_flags`
     - ``rst-text``

.. list-table:: Component discovery configuration

   * - Regular expression to match translation files against
     - ``docs/locales/(?P<language>[^/.]*)/LC_MESSAGES/(?P<component>[^/]*)\.po``
   * - Customize the component name
     - ``Documentation: {{ component|title }}``
   * - Define the base file for new translations
     - ``docs/locales/{{ component }}.pot``

.. hint::

   Would you prefer Sphinx to generate just single PO file? Since Sphinx 3.3.0
   you can achieve this using:

   .. code-block:: python

      gettext_compact = "docs"


You can find several documentation projects being translated using this approach:

* `Weblate documentation <https://docs.weblate.org/>`_ (you are reading that now)
* `Godot engine documentation <https://docs.godotengine.org/en/stable/>`_
* `Gallette documentation <https://doc.galette.eu/>`_
* `phpMyAdmin documentation <https://docs.phpmyadmin.net/>`_

.. _Sphinx: https://www.sphinx-doc.org/
.. _Read the Docs: https://readthedocs.org/
