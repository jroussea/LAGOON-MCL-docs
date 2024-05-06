Command line option
===================

LAGOON-MCL parameters
---------------------

Mandatory
~~~~~~~~~

* ``--fasta <path>``

Path to fasta files. It is necessary to indicate the name of the 
FASTA file. If there are several files use ``*.extension``.

.. code-block:: shell
    
    # #Example: 
    nextflow run main.nf [profile] --fasta $baseDir/tests/full/tr_files_test/*.fasta

* ``--annotation <path>``

| Path to sequence annotation files. You should not specify the name 
  of the file(s) but only the name of the folder containing the files.
| Exemple: ``--annotation $baseDir/tests/full/an_files_test``

* ``--pep_colname <str>``

| Name of the column containing the sequence names in the annotation 
  file(s). 
| Example: ``--pep_colname peptides``

* ``--columns_attributes <list>``

| Cette commande permet de sélectionner les colonnes qui vont être 
  utilisé comme label au moment de la construction des clusters
| Cette commande utilise une liste ou chaque colonne est séparé 
  par une vigule ``,``.
| Example: ``--columns_attributes identifiant,interproscan,go``

.. tip:: 

   | If two columns are linked, for example the database column 
     (contains the names of the databases: Pfam, CATH, ...) 
     and the identifier (contains the identifiers specific to 
     the databases) it is necessary to separate them by ``-``.
   | Exemple: ``--columns_attributes database-identifiant,interproscan``


Optional
~~~~~~~~

* ``--projectName <str>``

Default: ``LAGOON-MCL``

| Name of the project il est utilisé comme nom pour le dossier 
  contenant les fichiers temporaire.
| Il peut être retouvé dans le dossier : ``workdir/$projectName``

* ``--outdir <path>``

Default: ``"$baseDir/results"``

Path to the folder containing the results. Ce dossier contiendra
Tous les dossiers et fichiers de sortie de LAGOON-MCL.

* ``--concat_fasta <str>``

Name of the file that will contain all the fasta sequences.


* ``--information <true or false>``

Default: ``false``

Specify ``true`` if you have a ``TSV`` file which contains information 
that applies to all sequences in a file.

.. note:: 
  Si ``true``, il est obligatoire d'utiliser les paramètres 
  ``--information_files`` et ``--information_attributes``.

* ``--information_fils <path>``

Mandatory if ``--information true``

| Path to the TSV file containing general information about each 
  FASTA file. One line in the TSV file corresponds to one 
  FASTA file. 
| Example: if you have 30 FASTA files containing the genomes of 
  30 different species (1 file = 1 species) then the TSV file will 
  contain 30 lines. For example, each line can correspond to the 
  taxonomy of each species. 
| L'obejectif de ce fichier est d'appliquer toutes les informations
  qu'il contient sur l'entiereté d'un fichier fasta. Cela permet 
  d'éviter de les mettre dans les fichiers d'annotation et d'avoir
  potentiellement de nombreuse ligne avec de nombreuses informations
  manquante (dans le cas ou c'est ligne ou séqunece n'aurait pas 
  était annoté fonctionnellement)

.. warning::

    The first column contains the FASTA file name 
    (without the ``.fasta`` extension).

.. warning:: 
    
    It is possible to specify only one TSV file with this option 

* ``--information_attributes <list>``

Mandatory if ``--information true``

This option is identical to the ``--columns_attributes`` option.
For more information, see ``--columns_attributes``.

Diamond parameters
------------------

* ``--run_diamond <true or false>``

Default: ``true``

If ``false``, use parameter ``--diamond`` (to supply the alignment file). 
Parameters ``--diamond_db``, ``--matrix``, ``--sensitivity`` and 
``--diamond_evalue`` are not used.

* ``--diamond <str or path>``

Default: ``diamond_alignment.tsv``

| Nom du fichier qui contiendra les alignements issus de Diamond BLASTp.
| Si vous avez utilisé la commande ``--run_diamond false``, alors cette
  option vous permettra d'indiquer le chemin vers votre fichier d'alignement.

* ``--sensitivity <str>``

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

* ``--matrix <str>``

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

.. tip::

  vous pouvez utiliser ``--run_mcl false`` si vous voulez tester
  préalablement différents paramètres pour Diamond BLASTp.


* ``--I <list>``

Default: ``1.4,2,4``

List des différents paramètres d'inflations que vous voulez utiliser
pour le clustering. Il faut séparer chaque paramètre par une virgule ``,``.
Il est également possible de sépcifier des foat, le séparateur décimal
doit être un point ``.``, par exemple : 1.4.

For more information, see the `MCL documentation <https://micans.org/mcl/>`__.

.. note:: 

  Vous pourrez comparer chaque clustering réalisé grace aux différents
  score que fourni LAGOON-MCL, notamment le score d'homogénéité, qui 
  est calculé pour chaque attribut fournis avec les options : 
  ``--columns_attributes`` et ``--information_attributes``.

* ``--max_weight <float>``

Default: ``350``

Maximum weight for edges. This allows you to avoid having stops 
with infinite weight. Because the values are transformed into negative 
log 10.