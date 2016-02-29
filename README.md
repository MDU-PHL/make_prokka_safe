# `make_prokka_safe`: a tool to quickly transform your reads into a format that is safe for `prokka`

## Motivation

When annotating `prokka` will fail if the contig name, or locus-tag exceed a certain number of characters.
This will not be a problem for MDU IDs, but may occur with read sets with other naming conventions. So, 
what this little does is create a nullarbor input that names your reads in a fashion similar to MDU IDs. 
These have the format XXXX-XXXXX, and the goal is to get your reads to be named in a similar format
without actually renaming them.

## Input

The script takes as input a folder containing reads, each in a subfolder named after the isolate:

	my_reads/
		isolate1_09181777/isolate1_09181777_R1_fastq.gz

As an option, the script takes a prefix of maximum 4 characters (the default is 2016), but it could be
anything (e.g., 'MYRD').

## Output

The script will produce a `input.tab` file which can be used directly in `nullarbor`. The script will
generate `symlinks` in the individual isolate folders so that the read names are renamed according to 
the new isolate ID. The original isolates  are sorted alphabetically/numerically, and then relabelled 
in the `input.tab` file:

So, the isolate above would look like this in the `input.tab`:

	MYRD-00001	my_reads/MYRD-00001_R1.fastq.gz	my_reads/MYRD-00001_R2.fastq.gz

And, in the subfolder for the isolate, you will find symlinks to the original read files relabelled
accordingly.

## The command for the above

	make_prokka_safe --prefix MYRD my_reads 

## Requirements

	Python 2.7.x
	Click 6.0.x

 
