Call Pilon (2)
----------

Start Pilon with::

  java -Xmx32G -jar pilon-1.23.jar

and the following parameters:

+------------------------------------------+----------------+-------------------------------------------------------------------+
| What?                                    | parameter      | Our value                                                         |
+==========================================+================+===================================================================+
| The consensus sequence                   | --genome       | ~/workdir/results_artic/barcode_01.consensus.fasta                |
+------------------------------------------+----------------+-------------------------------------------------------------------+
| The input mapping                        | --frags        | ~/workdir/mappings/Illumina_vs_consensus_01.sorted.bam            |
+------------------------------------------+----------------+-------------------------------------------------------------------+ 
| The output prefix                        | --output       | ~/workdir/results_artic/barcode_01_pilon                          |
+------------------------------------------+----------------+-------------------------------------------------------------------+
| The number of threads to be used         | --threads      | 14                                                                |
+------------------------------------------+----------------+-------------------------------------------------------------------+
| Generate a file with changes             | --changes                                                                          |
+------------------------------------------+----------------+-------------------------------------------------------------------+

Make sure, to enter the resuls_artic directory first::

  cd ~/workdir/results_artic/

The complete command is::

  java -Xmx32G -jar ~/pilon-1.23.jar --genome ~/workdir/results_artic/barcode_01.consensus.fasta --changes --frags ~/workdir/mappings/Illumina_vs_consensus_01.sorted.bam --threads 14 --output ~/workdir/results_artic/barcode_01_pilon
  
**Perform that step for the first (01) dataset only to save time. Do the other datasets later, when there is time left.**

A loop to do that for all samples would look like this::

  for i in {1..5}
  do
  java -Xmx32G -jar ~/pilon-1.23.jar --genome ~/workdir/results_artic/barcode_0$i.consensus.fasta --changes --frags ~/workdir/mappings/Illumina_vs_consensus_0$i.sorted.bam --threads 14 --output ~/workdir/results_artic/barcode_0$i_pilon
  done

Inspect the ``barcode_01_pilon.changes`` file to see what has been corrected. Usually, you would do several rounds of Pilon until there are no further changes in the changes file. You would need to map the Illumina reads again vs the Pilon-polished consensus sequene, run Pilon, map again, and so on.

We will now just use our first round Pilon polished consensus sequences and put them into nextstrain.

References
^^^^^^^^^^

**pilon** https://github.com/broadinstitute/pilon/wiki

