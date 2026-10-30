Using AI
========

AI coding assistants can draft *Carob* scripts, but they do not replace a person. The human who submits the script is responsible for every line of code, every comment, and every mapping. Do not trust generated output. Review it against the raw data and, if there is one, the associated publication.

The rules for scripts are the same as when you write them by hand. Read the `guidelines <./guidelines.html>`_ and the `example script <./example.html>`_ first.


Tell the agent what to read
---------------------------

Put the agent in a clone of the `carob repo <https://github.com/carob-data/carob/>`_ so it can see existing scripts. Then tell it to read ``AGENTS.md`` in the root of that repo (also `on GitHub <https://github.com/carob-data/carob/blob/main/AGENTS.md>`__). That file is the instruction set for drafting scripts: vocabulary, metadata, units, testing, and what not to invent.

If the agent has not read ``AGENTS.md``, it will guess names, invent fertilizer rates, and skip comments. Point it there explicitly, for example:

.. code:: text

   Read AGENTS.md and draft a Carob script for doi:10.7910/DVN/XXXXXX
   in the agronomy group. 


A practical workflow
--------------------

1. **Pick a dataset** that is not already done. Use the `to-do list <./todo.html>`_, `Gardian <https://gardian.cgiar.org>`_, or a URI you care about. Check ``carobiner::on_github`` before you start.

2. **Set up as usual**: install *R* and *carobiner*, fork and clone the repo (see `Contribute <./index.html>`_ and `git <./git.html>`_).

3. **Ask the agent to draft the script** for one URI and one group. It should start with ``carobiner::draft(uri, path, group)``, inspect the downloaded files, copy the title and abstract into the script, and map columns to the `terminag <https://controvoc.github.io/terminag/>`_ vocabulary.

4. **Run the script yourself** in a clean *R* session and read every message from ``carobiner::write_files``. Ask the agent to fix real problems. Do not let it hide warnings (``suppressWarnings``, filtering "numeric-looking" text, dropping rows just to silence a message).

5. **Read the whole script**. Check ``## NOTES`` and ``## ISSUES`` against the data and the paper. Wrong notes are worse than an honest "I could not determine this".

6. **Fill in** ``carob_contributor`` with **your name** (a real person — never the model). The model name belongs in ``carob_LLM``. Then commit and open a **single-file** pull request as usual.


What AI gets wrong
------------------

These come up often. Watch for them:

* Inventing values that are not in the data or the paper (N/P/K rates, planting dates, coordinates, yield moisture).
* Putting the dataset in the wrong group (for example treating a field experiment as a household survey).
* Mapping an unknown term to ``"none"`` or ``"unknown"`` only to clear a vocabulary warning. Keep the real value and leave the warning.
* Dropping a useful variable because it is not yet in terminag. Keep it, with a trailing underscore if needed, and note it.
* Filling ``carob_contributor`` with the model name, a placeholder, or a GitHub handle.
* Guessing georeferences. Estimated coordinates must be documented; if they cannot be found, leave them ``NA``.
* Treating a first draft as finished. Unreviewed scripts do not belong in ``scripts/<group>/`` and should not be submitted as a pull request.


What you must not skip
----------------------

Before you open a pull request:

* You have read every line of code and every comment.
* Title and abstract in the script match the source.
* Treatments and responses are not swapped; units are standard (yield in kg/ha, fertilizer as elemental N, P and K).
* Remaining ``write_files`` messages are listed in the PR, with a short reason if they cannot be fixed.
* The commit message follows ``<new|edited> <group> script <uri>``.

If you cannot check a claim, leave it in ``## ISSUES`` rather than guessing. An unanswered question is better than a guess that looks correct.
