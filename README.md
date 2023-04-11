# lexical_restriction

Used for restricting an n-gram feature set (i.e. a lexicon) by only keeping ngrams that occur with similar frequency, according to both binomial (count) and boolean (zero-inflation) distribution statistics for both datasets (`source` and `target`).

Default output is list of filtered ngrams with their statistics. 

The Default frequency thresholds are ones found somewhat effective 
for adapting from social media (Facebook) to spoken language 
(oral history interviews). 
If specifying `--output_stats` then statistics for every ngram 
that appears in both the source feature table and target feature 
table will be output so one can then threshold to select features.

## Basic Examples:

Using csvs:
```
python3 ngram_restriction.py --source_csv /data/DIR/SOURCE_NGRAM_TABLE.csv \
                             --target_csv /data/DIR/TARGET_NGRAM_TABLE.csv \
                             [--filter_csv LEXICON] \
                             --output_stats --debug --output /data/DIR/WORD_STATS.csv
```

Using mysql
```
python3 ngram_restriction.py --source_db SDB --source_table SOURCE_NGRAM_TABLE \
                             --target_db TDB --target_table TARGET_NGRAM_TABLE \
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
                        Optional flag to pass in an `allowlist' of ngrams (i.e. a lexicon). 
  --filter_csv_colname FILTER_CSV_COLNAME
                        The column from filter_csv that contains the ngrams.
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
