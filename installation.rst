Installation
============

Requirements
------------

LAGOON-MCL uses `NextFlow <https://www.nextflow.io/>`__ as a workflow 
manager and `Singularity <https://sylabs.io/singularity/>`__ or
`Conda <https://conda.io/projects/conda/en/latest/user-guide/install/
index.html>`__ for the use of different tools.

.. note::

   This workflow is developed with:
    * NextFlow = 23.10.0.5889
    * Conda = 24.1.2
    * Singularity = 4.1.0.

Linux systeme
-------------

The pipeline was tested on Ubuntu 20.04 and Ubuntu 22.04.

With Conda
~~~~~~~~~~

1. Install `NextFlow <https://www.nextflow.io/docs/latest/getstarted.html#installation>`_ 
2. Install `Conda <https://conda.io/projects/conda/en/latest/user-guide/install/index.html>`_
   (`Anaconda <https://www.anaconda.com/download>`_ or `Miniconda <https://docs.anaconda.com/free/miniconda/>`_)
3. Download last release:

.. code-block:: shell

    git clone https://github.com/jroussea/lagoon-mcl.git
    cd lagoon-mcl

4. Test the pipeline on a minimal dataset

.. code-block:: shell
    
    nextflow run main.nf -profile test_full,conda

With Singularity
~~~~~~~~~~~~~~~~

1. Install `NextFlow <https://www.nextflow.io/docs/latest/getstarted.html#installation>`_ 
2. Install `Singularity <https://docs.sylabs.io/guides/4.1/user-guide/quick_start.html#quick-installation-steps>`_
3. Download last release:

.. code-block:: shell

    git clone https://github.com/jroussea/lagoon-mcl.git
    cd lagoon-mcl

4. Build containers

.. code-block:: shell

    bash singularity_containers.sh

5. Test the pipeline on a minimal dataset

.. code-block:: shell
    
    nextflow run main.nf -profile test_full,singularity

.. note::

   If you get a ``permission denied`` when you run the workflow, you'll 
   need to assign execution rights to the various scripts in the ``bin/`` 
   folder.

   .. code-block:: shell

    chmod +x bin/*

Shiny application
-----------------

In order to interactively explore the results obtained with LAGOON-MCL, 
I am currently developing a R Shiny application. It is available on 
`GitHub <https://github.com/jroussea/LAGOON-MCL-Shiny-app>`_.