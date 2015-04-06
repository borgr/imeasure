
#Contents

This package contains a Python implementation of the *I-measure* used for evaluating grammatical error correction systems. A full description of the method can be found in the following paper, which should be cited when using the script.

```Mariano Felice and Ted Briscoe. 2015. Towards a standard evaluation method for grammatical error detection and correction. In Proceedings of the 2015 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies (NAACL-HLT 2015), Denver, CO. Association for Computational Linguistics. (To appear)```

#Requirements

This scripts were coded in Python 2.7 and require the `xml.etree.cElementTree` library (usually shipped with Python by default).

#Usage

##Simple usage

You can evaluate a system's output by issuing the following command:

`python ieval.py -hyp:*system_output_file* -ref:*gold_standard_file*`

where *system_output_file* is the plain text output produced by an error correction system and *gold_standard_file* is an XML-formatted gold-standard file containing each source sentence with its errors and corrections. You can test the script using the example files provided, e.g.:

`python ieval.py -hyp:example/sys.txt -ref:example/gold.xml`

This will print a table showing the results for the whole input corpus. Apart from the I-measure, the output will include complementary counts and measures that are useful for comparison and error analysis.

##Options

The full set of options accepted by the evaluation script is as follows:

python ieval.py -ref:<file> -hyp:<file> [-nomix] [-max:<metric>] [-opt:sent|corpus] [-b:<n>] [-w:<n>] [-per-sent] [-v] [-vv]

where:

-ref   : XML file containing gold standard annotations.
-hyp   : Plain text file containing sentence hypotheses (one per line).
-nomix : Do not mix corrections from different annotators; match the best individual reference instead.
         By default, the scorer will mix such corrections in order to maximise matches. This option disables 
         default behaviour.
-max   : Maximise scores for the specified metric: dp, dr, df, dacc, dwacc, di, cp, cr, cf, cacc, cwacc or ci.
         Preceding 'd' is for detection, 'c' for correction. Available metrics are: tp (true positives), 
         tn (true negatives), fp (false positives), fn (false negatives), p (precision), r (recall), 
         f (F measure), acc (accuracy), wacc (weighted accuracy), i (improvement on wacc). Default is ''' + max_a + max_m + '''.
-b     : Specify beta for the F measure. Default is *1.0*.
-w     : Specify weight of true and false positives for weighted accuracy. Default is *2.0*.
-per-sent : Show individual results for each sentence.
-opt   : Optimise scores at the sentence or corpus level. Default is *sent*.
-v     : Verbose output.
-vv    : Very verbose output.

#Gold standard file format
