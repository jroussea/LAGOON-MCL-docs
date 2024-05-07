# LAGOON-MCL documentation

To contribute to the documentation

1. Clone the repository
2. Inside the downloaded directory, create an virtual environment using the commande `python -m venv myvenv`.
3. Activate the environment `source myvenv/bin/activate`
4. Install requirements `pip install -r requirements.txt`

The documentation is written in [reStructuredText (RST)](https://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html).

To view the documentation before making a `git push`, you must compile the rst code in html with :

```bash
make html
```

To view the documentation, you can view the html code in a browser.

```bash
firefox build/html/index.html
```

WARNING: don't `git push` files in the build folder..

The documentation is then compiled and put online with [Read the Docs](https://about.readthedocs.com/?ref=readthedocs.com)

access to documentation: [https://lagoon-mcl-docs.readthedocs.io/en/latest](https://lagoon-mcl-docs.readthedocs.io/en/latest)

