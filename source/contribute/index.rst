
Contribute
==========


*Carob* is an open-source community project to standardize and compile agricultural research data. You are invited to **contribute** to *Carob* by contributing `R` scripts for datasets of interest, or by improving existing scripts. All scripts are available on `github <https://github.com/carob-data/carob/>`_ (in the ``scripts`` folder).

To contribute you can follow these steps


1. **Install** the current version of `R <https://cran.r-project.org/>`__ and `git <https://git-scm.com/downloads>`__. You can also install `R-Studio <https://posit.co/download/rstudio-desktop/>`__.
2. In *R*, **install** the "carobiner" package with ``remotes::install_github("carob-data/carobiner")`` (you may need to first run ``install.packages("remotes")``).
3. **fork** the *Carob* `repo <https://github.com/carob-data/carob/>`_ to your github account. 
4. **clone** the forked repo to your computer.
5. create a new `R` **script**, or make the changes to an existing script. See this `example <./example.html>`__ and the `guidelines  <./guidelines.html>`_. You can use `AI to help draft a script <./ai.html>`__.
6. **check** your work by running ``carobiner::run_carob()`` for the new or changed `R` script.
7. **sync** the forked repo with main repo in carob-data/carob such that your fork is not behind.
8. **add** and/or **commit** these changes to the forked repo on your github account.
9. **push** your changes to the forked repo on your github account.
10. create a **pull request** to integrate your changes into the main repo. Keep pull requests simple. They should normally consist of only one file at a time. 

If you are not familiar with these procedures you can try to follow `these instructions <./git.html>`__. 

If you find this procedure too daunting we can also try to work with you in other ways. You can write to us using this `contact form <../contact.html>`__, or raise an `issue <https://github.com/carob-data/carob/issues>`_ on github.

You can discover new data sets with the `Gardian <https://gardian.cgiar.org>`_ search engine. You can also look at our `to-do list <./todo.html>`__ for ideas. You can check our `done list <../data/done.html>`_ to make sure you do not work on a dataset that has already been processed). But since there can be a delay in updating what is shown here, before you start working on a dataset, you should check with ``carobiner::on_github`` if it has already been done (and has been added to the github repo). You can also help fix some of the remaining `issues <./issues.html>`__.



.. toctree::
	:hidden:
	:maxdepth: 3
	
	git
	example
	guidelines
	ai
	georeference
	todo
	issues