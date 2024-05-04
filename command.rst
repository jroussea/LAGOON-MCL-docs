Command line option
===================

LAGOON-MCL parameters
---------------------

Mandatory
~~~~~~~~~

* ``--fasta <file>``

| Path to fasta files. It is necessary to indicate the name of the 
  FASTA file. If there are several files use ``*.extension``.
| Example: ``"$baseDir/tests/full/tr_files_test/*.fasta"``

* ``--annotation <file>``

| Path to sequence annotation files. You should not specify the name 
  of the file(s) but only the name of the folder containing the files.
| Exemple: ``"$baseDir/tests/full/an_files_test"``

* ``--pep_colname <string>``

| Name of the column containing the sequence names in the annotation 
  file(s).
| Example: ``"peptides"``

* ``--columns_attributes <string>``

| Name of the columns that will be used to annotate the networks. 
| Each column name must be separated by a ``,``.
| Example: ``"database-identifiant,go"``

.. tip:: 

   If two columns are linked, for example the database column 
   (contains the names of the databases: Pfam, CATH, ...) 
   and the identifier (contains the identifiers specific to 
   the databases) it is necessary to separate them by ``-``.

Optional
~~~~~~~~

* ``--projectName <string>``

Default: ``LAGOON-MCL``

Name of the project 

* ``--outdir <path>``

Default: ``"$baseDir/results"``

Path to the folder containing the results.

* ``--concat_fasta <string>``

Name of the file that will contain all the fasta sequences.

* ``--concat_fasta <true or false>``

Default: ``false``

Specify ``true`` if you have a ``TSV`` file which contains information 
that applies to all sequences in a file.

.. note:: 
    If ``true``, use parameters ``--information_files`` 
    and ``--information_attributes`` parameters.

* ``--information_fils <path>``

Mandatory if ``--information true``

| Path to the TSV file containing general information about each 
  FASTA file. One line in the TSV file corresponds to one 
  FASTA file. 
| Example: if you have 30 FASTA files containing the genomes of 
  30 different species (1 file = 1 species) then the TSV file will 
  contain 30 lines. For example, each line can correspond to the 
  taxonomy of each species. 

.. warning::

    The first column contains the FASTA file name 
    (without the ``.fasta`` extension).

.. warning:: 
    
    It is possible to specify only one TSV file with this option 

* ``--information_attributes <string>``

Mandatory if ``--information true``

This option is identical to the ``--columns_attributes`` option.
For more information, see ``--columns_attributes``.

Diamond parameters
------------------

* ``--run_diamond <true or false>``

Default: ``true``

If false, use parameter ``--diamond`` (to supply the alignment file). 
Parameters ``--diamond_db``, ``--matrix``, ``--sensitivity`` and 
``--diamond_evalue`` are not used.

* ``--diamond <path or name>``

Default: ``diamond_alignment.tsv``

Name of the file containing the pairwise alignment from Diamond blastp.

Used to indicate the path to the alignment file if ``--run_diamond false``.

* ``--sensitivity <sensitivity>``

Default: ``sensitive``

.. list-table:: Diamond sensitivity setting

    * - fast
      - mid-sensitive
      - more-sensitive
      - very-sensitive
      - sensitive
      - ultra-sensitive

For more information, see the `Diamond documentation <https://github.com/
bbuchfink/diamond/wiki/3.-Command-line-options#sensitivity-modes>`_ .

* ``--matrix <matrix>``

Default: ``BLOSUM62``

.. list-table:: Matrix used for alignment

    * - BLOSUM45
      - BLOSUM50
      - BLOSUM62
      - BLOSUM80
      - BLOSUM90
      - PAM250
      - PAM70
      - PAM30
  
For more information, see the `Diamond documentation <https://github.com/bbuchfink/diamond/wiki/3.-Command-line-options#alignment-options>`__.

* ``--diamond_evalue <int>``

Default: ``0.001``

Evalue used by diamond blastp. 

For more information, see the `Diamond documentation <https://github.com/bbuchfink/diamond/wiki/3.-Command-line-options#output-options>`__.

MCL parameters
--------------

* ``--run_mcl <true or false>``

Default: ``true``

Running Markov CLustering algorithm.

* ``--I``

Default: ``1.4,2,4``

Inflation parameter list for Markov CLustering algorithm. It is 
possible to specify several inflation parameter. In this case it 
separates them by ``,``.

For more information, see the `MCL documentation <https://micans.org/mcl/>`__.

* ``--max_weight``

Default: ``350``

Maximum weight for edges. This allows you to avoid having stops 
with infinite weight. Because the values are transformed into negative 
log 10.