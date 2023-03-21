# lexical_restriction

Used for restricting an n-gram feature set by only keeping tokens that occur similarly
frequently, according to both binomial (count) and boolean (zero-inflation), 
in distributions of both datasets.

Output is statistics for every token that appears in both the source feature table 
and target feature table. The statistics can then be thresholded to select features.

## Basic Example:
```
python3 ngram_restriction.py --source_csv /data/DIR/SOURCE_MSG_TABLE.csv 
                             --target_csv /data/DIR/TARGET_MSG_TABLE.csv 
                             --output_stats --debug --output /data/DIR/WORD_STATS.csv
```

## All Argument Descriptions
```
optional arguments:
  -h, --help            show this help message and exit
  --source_db SOURCE_DB
                        Source db in mysql. If specified, a source table is
                        also required.
  --target_db TARGET_DB
                        Target db in mysql. If specified, a target table is
                        also required.
  --source_table SOURCE_TABLE
                        Source table in mysql. If specified a source db is
                        also required.
  --target_table TARGET_TABLE
                        Target table in mysql. If specified a target db is
                        also required.
  --freq_variable FREQ_VARIABLE
                        Variable from table to use for frequency.
  --sparse_threshold SPARSE_THRESHOLD
                        Sparse filter threshold. Entries are kept when their
                        binary usage (whether they occur are not) between
                        source and target are within sparse_threshold
                        multiples of eachother.
  --stdev_threshold STDEV_THRESHOLD
                        Standard Deviation threshold. Keep words that are
                        within {stdev_threshold}-sigma between the source and
                        target domain (with sigma calculated as the stdev on
                        the source domain for that token).
  --output OUTPUT       File to output the set of remaining n-grams to. If not
                        specified, will be flushed to stdout.
  --combined_feat_set COMBINED_FEAT_SET
  --filter_csv FILTER_CSV
                        A csv where the FEAT column gives a list of valid
                        tokens
  --filter_csv_colname FILTER_CSV_COLNAME
                        Column name for filter csv
  --zero_removed ZERO_REMOVED
                        For the stdev threshold, determines whether or not to
                        reweight mean and variance to ignore zero entries.
  --source_csv SOURCE_CSV
                        Source CSV, formatted like a dlatk table.
  --target_csv TARGET_CSV
                        Target CSV, formatted like a dlatk table.
  --source_dir SOURCE_DIR
                        Source CSV directory, with each file formatted like a
                        dlatk table.
  --target_dir TARGET_DIR
                        Source CSV directory, with each file formatted like a
                        dlatk table.
  --output_stats        Return scores rather than prefiltering.
  --debug               Enable debug output 
```
