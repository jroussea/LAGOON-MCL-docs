Installation requirements
=========================

LAGOON-MCL has been developed to run on Linux systems. No 
version has yet been tested on Windows or Apple (Mac OS X) 
operating systems, but it may be possible to run it on Apple 
operating systems using Conda.

Software requirements:
 * 64-bits Linux
 * `NextFlow <https://www.nextflow.io/>`__ 
 * `Conda <https://conda.io/projects/conda/en/latest/user-guide/install/index.html>`__
 * `Singularity <https://sylabs.io/singularity/>`__

You can run LAGOON-MCL with Conda or Singularity.

.. note::

   Ce workflow est développé:
    * NextFlow, version 23.10.0.5889
    * Conda, version 24.1.2
    * Mamba, version 1.5.8
    * Singularity, version 4.1.0.

Linux systeme
-------------

The pipeline was tested on Ubuntu 20.04 and Ubuntu 22.04.

Conda
~~~~~

1. Install `NextFlow <https://www.nextflow.io/docs/latest/getstarted.html#installation>`_
2. | Install `Conda <https://conda.io/projects/conda/en/latest/user-guide/install/index.html>`_
   | For Conda : `Anaconda <https://www.anaconda.com/download>`_ 
     or `Miniconda <https://docs.anaconda.com/free/miniconda/>`_
3. Download last release:

.. code-block:: shell

    git clone https://github.com/jroussea/lagoon-mcl.git
    cd lagoon-mcl

4. Test the pipeline on a minimal dataset

.. code-block:: shell
    
    # With conda
    nextflow run main.nf -profile test_full,conda

Singularity
~~~~~~~~~~~

1. Install `NextFlow <https://www.nextflow.io/docs/latest/getstarted.html#installation>`_ 
2. Install `Singularity <https://docs.sylabs.io/guides/4.1/user-guide/quick_start.html#quick-installation-steps>`_
3. Download last release:

.. code-block:: shell

    git clone https://github.com/jroussea/lagoon-mcl.git
    cd lagoon-mcl

4. | Build containers
   | For the moment, it's necessary to build the Singularity containers. 
     A bash script is available for this purpose.
   
   | You can find the Singularity Definition File in containers/singularity. 
     Once created, the containers will be available in the same folder.

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

Jupyter Notebook environment
----------------------------

Jupyter Notebook is used with the ``lagoon-mcl-jupyter.yaml`` environment. To do this, run the command :

.. code-block:: shell

    mamba env create -f lagoon-mcl-jupyter.yaml

    # OR

    conda env create -f lagoon-mcl-jupyter.yaml

Shiny application
-----------------

In order to interactively explore the results obtained with LAGOON-MCL, 
I am currently developing a R Shiny application. It is available on 
`GitHub <https://github.com/jroussea/LAGOON-MCL-Shiny-app>`_.