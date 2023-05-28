.. post:: 2023-03-25
   :tags: python, documentação, sphinx, autodoc, read the docs
   :category: blog, en
   :author: me
   :language: en


.. definição de box para incluir html snippets

.. raw:: html

    <style>
    .my-box {
    border: 1px solid #ddd;
    border-radius: 6px;
    padding: 10px;
    margin-bottom: 10px
    }
    </style>


Using Sphinx for generating documentation for Python software
*************************************************************


Documentation is an essential aspect of any software project. It serves as a source of information for end users and as a resource for developers who need to understand how the software works. Additionally, well-written documentation helps avoid maintenance issues in the future (i.e., avoiding technical debt) and improves the overall quality of the software.

In this article, I provide a practical example of how to create documentation (section :ref:`Example <example>`). I use `Sphinx`_ as the main tool for generating documentation and the `Read the Docs`_ repository for publishing it.

I demonstrate how to use the `autodoc`_ extension to enable automatic creation of the API, which extracts information from the code's docstring automatically (section :ref:`Automatic API Creation <automatic-api-creation>`). To change the default theme to one that offers a more visually pleasing appearance, I use the `sphinx_rtd_theme`_ extension (section :ref:`Defining the Documentation Theme <defining-documentation-theme>`). I also show how to publish the created documentation on `Read the Docs`_ (section :ref:`Publishing on Read the Docs <publishing-read-the-docs>`), allowing users to easily access the documentation through the web.

Additionally, I mention several Sphinx extensions (section :ref:`Other Sphinx Features <other-sphinx-features>`), both those included by default in Sphinx and others created by third parties and available on `PyPI`_. These extensions provide extra functionality for the documentation, making it more versatile and useful for different types of projects.

Sphinx and Read the Docs
========================

Sphinx
------

One of the most popular tools for creating documentation in Python projects is the `Sphinx`_ library. Sphinx is an open-source documentation tool that is easy to use and highly configurable. It uses the `ReStructuredText`_ (or RST) markup format, which is a lightweight and easy-to-learn markup language, to create the documentation.

One of the great advantages of Sphinx is its ability to automatically generate API documentation from the code's own documentation. This means that by writing code documentation, the API reference can be automatically generated from that documentation, saving time and effort in creating the documentation.

Another major advantage of Sphinx is its ability to generate documentation in various formats, such as HTML, PDF, and EPUB.

Read the Docs
-------------

Sphinx can also be easily integrated with `Read the Docs`_, an online documentation hosting service. The integration of Sphinx with Read the Docs allows the documentation to be easily published and accessible to all project users. Additionally, `Read the Docs for Business`_ allows private projects to use the platform, keeping the documentation private and secure.

Structure of Documentation
==========================

Basic Sections
--------------

Documentation can include various sections, such as getting started, user guide, API, and development. I describe the information contained in each section below.

- Getting Started: An overview of the library, demonstrating how to quickly and efficiently use it.
- User Guide: More detailed usage examples, with step-by-step explanations for utilizing the library.
- API: Detailed descriptions of the different functionalities and methods of the library.
- Development: Information on contributing to the development of the library, including details on coding standards, code structure, and testing.

Business Information
----------------------

In the case of internal documentation for the team, it may be interesting to add sections that address business aspects of the team, such as project objectives, contributors, financial information, clients, planning and long-term goals, meeting history, and requirements documentation. The sections vary between projects, and it is up to the team to define the necessary information for the documentation, taking into account the unique aspects of each project.

Other Documentation Channels
----------------------------

It is worth noting that while many project progress-related information needs to be documented, much of it is documented through management features included in code repositories, such as GitHub and GitLab. This information includes issues, release history, information related to each sprint and deliverable, and more.

.. _example:

Example
=======

In this example, I will use the `log_decor`_ library (v1) - an open-source logging decorator library that I recently developed - to demonstrate how to use Sphinx, in conjunction with the online hosting service `Read the Docs`_, to generate and publish the documentation for a Python application.

In this text, I would like to share a practical example of how to use the Sphinx library together with the Read the Docs online documentation hosting service to create and publish the documentation for a Python library. For this purpose, we will use the `log_decor`_ library, an open-source logging decorator library that I recently developed.

Before following the example on this page, I suggest you explore the `log_decor documentation on Read the Docs <https://log-decor.readthedocs.io/en/latest/index.html>`_. This will make it easier to understand the different points that will be covered.

Project Structure
-----------------

The directory structure of the **log_decor** library consists of several files and folders that are important for the development and documentation of the library. The structure and a brief description of each file and folder are presented below:

.. code-block::

    log_decor/
    ├── docs/
    ├── src/
    │   └── log_decor/
    |       ├── __init__.py
    |       └── ...
    ├── pyproject.toml
    └── requirements.txt


The ``docs/`` folder contains all the necessary files for creating the library's documentation.

The ``src/log_decor/`` folder contains all the source code files of the library. These files include the Python modules, as well as other files such as the ``__init__.py`` file, which indicates that the folder is a Python package.

The ``pyproject.toml`` file is used for installing the library. This file contains important information such as the name of the library, its version, and its dependencies.

Finally, the ``requirements.txt`` file in the project root lists the requirements necessary for the library to function.


Creating the Base Documentation Files
-------------------------------------

To create the base documentation files, simply execute the command

.. code-block::

    sphinx-quickstart


in the ``example_project/docs/`` directory. During the execution, the user is guided through a series of questions, such as the project name, the language used, the authors, and the version, among other options. These options are important to configure the documentation according to the project's needs.

When running the ``sphinx-quickstart`` command to create the library's documentation, some default files and folders are generated. These files are:

- ``conf.py``: the main configuration file for Sphinx, where general documentation settings are defined, such as the title, description, list of extensions, and other customization options.
- ``index.rst``: the main documentation file where the main topics are defined, such as the introduction, installation, and usage of the library. From this file, other documentation files are created.
- ``make.bat`` (for Windows) and ``Makefile`` (for Unix-based systems): script files used to compile the ``.rst`` files into HTML, PDF, and other formats.

After executing the command, the directory structure becomes as follows:

.. code-block::

    log_decor/
    ├── docs/
    |   ├── conf.py  # new
    |   ├── index.rst  # new
    |   ├── make.bat  # new
    |   └── Makefile  # new
    ├── src/
    │   └── log_decor/
    |       ├── __init__.py
    |       └── ...
    ├── pyproject.toml
    └── requirements.txt

Adding Content Files
--------------------

It is possible to write the documentation using multiple ``.rst`` files. In fact, it is a good practice to divide the documentation into different files, each with a specific focus, making it easier to navigate and read the content.

In the case of the example we are working on, we added several files in the ``docs/modules/`` folder that correspond to different sections of the documentation, which are displayed on different pages. Each file contains specific information about the subject covered in that section, allowing the reader to easily find what they are looking for.

The directory structure with the new files is as follows:

.. code-block::

    log_decor/
    ├── docs/
    |   ├── modules/  # new
    |   |   ├── api.rst
    |   |   ├── contributing.rst
    |   |   ├── examples.rst
    |   |   ├── license.rst
    |   |   └── usage.rst
    |   ├── conf.py
    |   ├── index.rst
    |   ├── make.bat
    |   └── Makefile
    ├── src/
    │   └── log_decor/
    |       ├── __init__.py
    |       └── ...
    ├── pyproject.toml
    └── requirements.txt

Writing the documentation's home page
-------------------------------------

The ``index.rst`` file is the main file of the documentation, where we define the basic structure and organization of the topics to be covered. It is responsible for importing the other ``.rst`` files that will compose the documentation, organizing them in a way that facilitates user navigation.

The ``index.rst`` serves as the home page of the documentation, as it is the first file the user accesses when opening the documentation. It is common to include a brief introduction of the project and a list of the topics that will be covered, so that the user can get a general idea of what they will find when browsing through the documentation.

Additionally, the ``index.rst`` can be used to include important information about the project, such as its license, credits to authors and contributors, links to the official project page, among other relevant information. All of this contributes to making the documentation more comprehensive and informative for users.

The ``index.rst`` file of the **log_decor** library is as follows:

.. code-block:: restructuredtext

    Welcome to log-decor's documentation!
    =====================================

    Introduction
    ############

    This package has class and method decorators that provide logging functionality.

    Getting Started
    ###############

    To install, execute the following command:

    .. code-block::

       pip install git+https://github.com/bernardopaulsen/log_decor.git


    .. toctree::
       :caption: Contents

       modules/usage
       modules/examples
       modules/api
       modules/contributing
       modules/license


    Indices and tables
    ==================

    * :ref:`genindex`
    * :ref:`modindex`
    * :ref:`search`


The different elements of the above file are:

- 'Welcome to log-decor's documentation!': Title of the homepage.
- 'Introduction': Section where a brief introduction about the library is presented, highlighting its main functionality.
- 'Getting Started': Section that provides the necessary information for users to start using the library. It includes an installation command using **pip** and a link to the GitHub repository.
- ``.. toctree::``: The command is used to create a table of contents for the generated documentation. It allows the user to list other ``.rst`` files that will be displayed in the table of contents.
- ``:caption: Contents``: Title that will be used for the table of contents.
- ``modules/usage``, ``modules/examples``, ``modules/contributing``, ``modules/license``: Links to the ``.rst`` files that will be included in the table of contents.
- ``Indices and tables``: Section that presents indexes and tables related to the documentation.
- ``:ref:genindex``: Link to the general index, which contains information about all documented modules, classes, and functions.
- ``:ref:modindex``: Link to the module index, which contains information about all documented modules.
- ``:ref:search``: Link to the search table, which allows users to search for any keyword in the documentation.

You can check the final result of this configuration below:

.. raw:: html
    :file: index-page.html

Note that the contents of the table of contents depend on the contents of each of the included ``.rst`` files in the table.

.. _automatic-api-creation:

Automatic API Creation
----------------------

The Sphinx `autodoc`_ extension allows documentation to be automatically generated from the library's source code. In our example, we are using this extension in conjunction with the `sphinx_autodoc_typehints`_ library (which adds support for automatically documenting argument types and return values of functions and methods) to automatically document classes and functions from our source code.

To configure the use of **autodoc** and **sphinx-autodoc-typehints**, they need to be included in the list of extensions in the ``conf.py`` file. Additionally, various options can be configured for the extensions, such as including private members, documenting attributes, and more.

Documentation written in the source code
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

There are several ways to document the source code, all described in the `autodoc`_ documentation. One of these ways is through *docstrings*, which are triple-quoted strings placed immediately after the definition of a function, method, class, or module. The *docstrings* can be read by the Sphinx **autodoc** extension and used to generate the documentation.

The following example is the ``add_logger.py`` module from the **log_decor** library:

.. code-block:: python

    # add_logger.py

    import functools
    import logging
    from typing import Optional, Type, TypeVar


    Class = TypeVar('Class')


    class AddLogger:
        """Class decorator that adds a logger attribute to the decorated class.

        :param name: Name of Logger. If None, the qualified name of the class
            passed to :meth:`add_logger.AddLogger.__call__` will be the name of
            the logger.
        """
        def __init__(self,
                    name: Optional[str] = None
                    ) -> None:
            self._name = name

        def __call__(self,
                    cls: Class
                    ) -> Type[Class]:
            """Add logger attribute to class.

            The name of the attribute will be '_logger'.

            :param cls: Class to which add logger. If no name was passed to
                :meth:`add_logger.AddLogger.__init__`, the qualified name of the
                class passed to this parameter will be the name of the logger.
            :return: Class with logger attribute.
            """
            @functools.wraps(cls,
                            updated=())
            class LoggedClass(cls):
                def __init__(self_,
                            *args,
                            **kwargs
                            ) -> None:
                    self_.logger = logging.getLogger(
                        name=self._name if self._name is not None else cls.__name__
                    )
                    super().__init__(*args,
                                    **kwargs)
            return LoggedClass


The *docstring* begins with a brief description of the object's function it is written for. Then, it provides descriptions of the object's parameters, and finally a description of the object's return value. It's worth noting that the descriptions of the parameters for the ``__init__`` method are written in the class's *docstring*, not in the method's *docstring*.

*Docstrings* can contain more information than just the simple description of the object and its parameters and return value. It is good practice to include usage examples of the object, examples of the relationship between arguments and return values, and other relevant information that can help the reader better understand how to use the documented object.

It is worth noting that the parameter types and return value types are not documented in the example's *docstrings*, but that is because the types are already documented in the code itself, and they will be read by the **sphinx_autodoc_typehints** extension and automatically added to the final documentation.

Setting up the source code directory
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

First, it is necessary to indicate the base directory of the library's source code by configuring the ``sys.path`` variable in the ``conf.py`` file. For example:

.. code-block:: python

    # -- Path setup
    import os
    import sys

    sys.path.insert(0, os.path.abspath('../src/log_decor'))


Defining the extensions
^^^^^^^^^^^^^^^^^^^^^^^

To add the **autodoc** and **sphinx_autodoc_typehints** extensions, they need to be added to the ``extensions`` list in the ``conf.py`` file. For example:

.. code-block:: python

    # -- General configuration
    extensions = [
        'sphinx.ext.autodoc',
        'sphinx_autodoc_typehints',
    ]


Adding automatic documentation of a class to a .rst file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To add the API documentation of a class to a ``.rst`` file, we can use the ``.. autoclass::`` directive. For example, to add the documentation of the ``AddLogger`` class from the ``add_logger`` module, we can use the following code:

.. code-block:: restructuredtext

    .. autoclass:: add_logger.AddLogger
       :members:
       :special-members: __call__

In the RST code above, the ``autoclass`` directive indicates that we are automatically documenting a class using the **autodoc** extension. The ``add_logger.AddLogger`` argument indicates the class we are documenting. The ``:members:`` option indicates that we want to document all members of the class, and the ``:special-members: __call__`` option indicates that we also want to document the special method ``__call__``, which is not documented by default by **autodoc** because it is a special method.

Below you can check the same result:

.. raw:: html
    :file: api-example.html

.. _defining-documentation-theme:

Defining the documentation theme
--------------------------------

Sphinx allows you to choose themes to customize the appearance of the documentation. The default Sphinx theme is **classic**, but there are several other themes available, such as **labaster**, **sphinx_rtd_theme**, and **sphinx_bootstrap_theme**, among others.

In the case of the **log_decor** library used as an example, the `sphinx_rtd_theme`_ theme was chosen, which is a popular and modern theme that offers a clean and professional look for the documentation.

The code required to configure the **sphinx_rtd_theme** theme in the ``conf.py`` file is as follows:

.. code-block:: python

    # -- Options for HTML output
    import sphinx_rtd_theme

    html_theme = 'sphinx_rtd_theme'
    html_theme_path = [sphinx_rtd_theme.get_html_theme_path()]


Installation of Required Libraries in the Development Environment
-----------------------------------------------------------------

To create documentation with Sphinx, both Sphinx and the auxiliary libraries need to be installed in the development environment. The auxiliary libraries required for generating the documentation are usually specified in a ``requirements.txt`` file, which should be located in the ``docs/`` directory. The libraries imported by the source code should also be installed since we are using the **autodoc** extension, but they are specified in the ``requirements.txt`` file in the project's root directory.

The directory structure will be as follows:

.. code-block::

    log_decor/
    ├── docs/
    |   ├── modules/
    |   |   └── ...
    |   ├── conf.py
    |   ├── index.rst
    |   ├── make.bat
    |   ├── Makefile
    |   └── requirements.txt  # new
    ├── src/
    │   └── log_decor/
    |       ├── __init__.py
    |       └── ...
    ├── pyproject.toml
    └── requirements.txt


The contents of the ``requirements.txt`` file will be:

.. code-block::

    sphinx
    sphinx_rtd_theme
    sphinx_autodoc_typehints


These packages can be installed with the command:

.. code-block::

    pip install --requirement docs/requirements.txt


Generating HTML Documentation
-----------------------------

Inside the ``docs/`` folder, the command

.. code-block::

    make html


is used to generate HTML documentation from the source files. The HTML files will be generated in the ``docs/_build/html`` directory by default. The documentation's main page is in the ``index.html`` file, which should be opened to access the documentation.

.. code-block::

    log_decor/
    ├── docs/
    |   ├── _build/  # new
    |   |   ├── doctrees/
    |   |   └── html/
    |   |        ├── ...
    |   |        ├── index.html
    |   |        └── ...
    |   ├── modules/
    |   |   └── ...
    |   ├── conf.py
    |   ├── index.rst
    |   ├── make.bat
    |   ├── Makefile
    |   └── requirements.txt
    ├── src/
    │   └── log_decor/
    |       ├── __init__.py
    |       └── ...
    ├── pyproject.toml
    └── requirements.txt


As mentioned earlier, the complete documentation can be accessed through the `log_decor page on Read the Docs <https://log-decor.readthedocs.io/en/latest/index.html>`_.

Sphinx also allows generating other types of documentation files, such as PDF and ePub. To generate a PDF file, for example, it is necessary to install LaTeX software and then use the command ``make latexpdf``. To generate an ePub file, the Calibre software needs to be installed, and the command ``make epub`` should be used.

.. _publishing-read-the-docs:

Publishing on Read the Docs
----------------------------

The integration between Sphinx, `GitHub`_, and Read the Docs is extremely useful for creating and maintaining up-to-date documentation for software projects. By using Sphinx to generate documentation from the source code and GitHub to store the code, it is possible to automate the process of updating the documentation with each new project version. And with integration with Read the Docs, the documentation can be easily hosted and shared with the community.

As mentioned earlier, the documentation for the **log_decor** project is available on Read the Docs at `its page on the platform <https://log-decor.readthedocs.io/en/latest/index.html>`_

Configuration
^^^^^^^^^^^^^

To integrate Sphinx with Read the Docs, it is necessary to configure a file called ``readthedocs.yaml`` in the project's root directory. This file allows specifying the Python version used in the documentation, as well as other configurations. For example, it is possible to specify the commands to be executed before building the documentation and the extensions to be used.

Below is the directory structure of the sample project after including the ``readthedocs.yaml`` file:

.. code-block::

    log_decor/
    ├── docs/
    |   └── ...
    ├── src/
    │   └── log_decor/
    |       ├── __init__.py
    |       └── ...
    ├── pyproject.toml
    ├── readthedocs.yaml  # new
    └── requirements.txt


The ``readthedocs.yaml`` file is as follows:

.. code-block:: yaml

    # readthedocs.yaml
    version: 2

    sphinx:
    builder: html
    configuration: docs/conf.py
    fail_on_warning: true

    python:
    version: 3.8
    install:
    - requirements: docs/requirements.txt
        extra_requirements:
        - requirements.txt


The file starts with the definition of the configuration file version, in this case, version 2.

The ``sphinx`` section is used to specify the Sphinx configurations. In this case, the defined builder is *html*, the configuration file used is ``docs/conf.py``, and ``fail_on_warning`` is set to **true**, which causes the documentation build process to fail if there are any warnings.

The ``python`` section is used to define the Python version that will be used to build the documentation and the list of packages that will be installed before the build. In this case, it is defined that version 3.8 will be used and that the files ``docs/requirements.txt`` and ``requirements.txt`` will be used to install the necessary packages, with the former defining the packages used by Sphinx and the latter defining the packages used by the source code of the library.

Integration with Read the Docs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Integrating `Read the Docs`_ with `GitHub`_ is straightforward and easy to set up. To create documentation on Read the Docs from a GitHub repository, simply create an account on Read the Docs, set up a new project, and link the project to the GitHub repository by selecting the repository and authorizing access. Once configured, Read the Docs will automatically monitor the GitHub repository for updates and generate a new version of the documentation whenever there is a new commit or pull request.

Accessing the Documentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Once the integration is set up and the documentation has been built, it can be accessed through the link provided by Read the Docs.

.. _other-sphinx-features:

Other Sphinx Features
=====================

Sphinx offers many features beyond documentation generation. Some of these features can make the documentation even more useful and accessible.

ReStructuredText
----------------

The ReStructuredText markup format itself has several features not demonstrated in the above example.

One of them is the `creation of links to sections and chapters of the documentation <https://docs.readthedocs.io/en/stable/guides/cross-referencing-with-sphinx.html>`_, including links to source code objects. These links can be included in the code's own docstrings, making the documentation even more interconnected and user-friendly.

Another feature worth mentioning is the `support for code blocks in the documentation <https://www.sphinx-doc.org/en/master/usage/restructuredtext/directives.html#showing-code-examples>`_ (including in docstrings), which allows usage examples of the library to be directly exposed in the documentation. This can be particularly useful in helping users understand how to use the library in their own projects.

Extensions
----------

In addition to the standard features, Sphinx also has several very useful extensions, both those included in the library and third-party extensions, which can further facilitate the documentation process and make the documentation richer and more comprehensive. Some of the included extensions in Sphinx are:

- `doctest <https://www.sphinx-doc.org/en/master/usage/extensions/doctest.html>`_: inclusion of unit tests within the documentation, making it more interactive and facilitating understanding of the library's usage.
- `intersphinx <https://www.sphinx-doc.org/en/master/usage/extensions/intersphinx.html>`_: inclusion of links to documentation of other libraries, facilitating access to the documentation of other tools.
- `viewcode <https://www.sphinx-doc.org/en/master/usage/extensions/viewcode.html>`_: inclusion of links to the source code of documented classes, functions, and methods, making the documentation more comprehensive and allowing for a deeper understanding of how the library works.

Some third-party extensions that can be easily installed and used with Sphinx and are available in the `PyPI`_ repository are:

- `sphinxcontrib-jupyter <https://pypi.org/project/sphinxcontrib-jupyter/>`_: inclusion of Jupyter notebooks in the documentation, making it more interactive and allowing for the visualization of usage examples of the library in a more dynamic way. It is worth noting that this extension is developed by the `QuantEcon organization <https://quantecon.org/>`_, which is an organization dedicated to economic modeling, providing libraries and educational materials on the subject, among other projects. I strongly recommend exploring the organization's projects if you are interested in economic modeling and quantitative finance.
- `sphinxcontrib-bibtex <https://pypi.org/project/sphinxcontrib-bibtex/>`_: automatic inclusion of bibliographic citations in the documentation, facilitating reference to articles and scientific works related to the library.

Conclusion
==========

In conclusion, documentation is a fundamental part of any software project, but unfortunately, it is often neglected by developers. Clear and well-written documentation not only helps to facilitate understanding of the project, but also eases the maintenance process and collaboration with other developers.

`Sphinx`_ is a powerful tool that makes documentation creation and maintenance much easier and efficient. Furthermore, integration with `GitHub`_ and `Read the Docs`_ enables simple and accessible sharing of the documentation with anyone interested in the project.

I hope you have enjoyed the article and that it has been useful in improving the documentation of your software projects. Always remember that good documentation is essential for the success of any project!

.. definições de links

.. _Sphinx: https://www.sphinx-doc.org/en/master/
.. _sphinx_rtd_theme: https://pypi.org/project/sphinx-rtd-theme/
.. _autodoc: https://www.sphinx-doc.org/en/master/usage/extensions/autodoc.html
.. _sphinx_autodoc_typehints: https://pypi.org/project/sphinx-autodoc-typehints/
.. _Read the Docs: https://readthedocs.org/
.. _Read the Docs for Business: https://about.readthedocs.com/?ref=dotcom-homepage
.. _log_decor: https://test.pypi.org/project/log-decor/
.. _ReStructuredText: https://www.sphinx-doc.org/pt_BR/master/usage/restructuredtext/basics.html
.. _GitHub: https://github.com/
.. _PyPI: https://pypi.org/