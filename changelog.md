# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)

## [Unreleased 0.4.99] - 2019-08-13
### Added
- Added the following steps to the main single-end pipeline:
  - sort_bed (sorts input normalized bed file)
  - blacklist remove (removes blacklisted regions from peak file)
  - bed to narrowPeak (converts peak bed file to narrowPeak format)
  - fix bed ("fixes" a peak bed file format such that it is compatible with bedToBigBed)
  - bed to bigbed (calls bedToBigBed to convert peak bed file to bigBed format)
- Added a 'nostats' workflow in 'wf/' to optionally run the pipeline without requiring umi_tools stats generation. This dramatically cuts down on runtime/mem reqs
- Added pre/post processing scripts (annotate_peaks_bedformat_wproxdistal_lncRNA.pl & generate_adaptertrim_fasta.ipynb)
  - annotate_peaks_bedformat_wproxdistal_lncRNA.pl (perl script that annotates bed files)
  - generate_adaptertrim_fasta.ipynb (jupyter notebook that generates fasta files w/ partial adapter sequences to trim)

## [0.4.0] - 2019-03-25
### Changed
- YAML metadata changes slightly to account for each dataset to potentially have its own adapter sequences

## [0.3.0] - 2019-03-05
- There is some work done to make the SE pipeline outputs deterministic. Outputs should be the same every time.
- Introducing a "wf_encode_full" workflow that combines the peak calling workflow, the repeat mapping workflow (hg19 only), and region-level normalization workflow
- The previous manifests (eCLIP-0.2.2) for eCLIP_pairedend and eCLIP_singleend should still work.

### Added
- gzip step for all fastq files
- added ```arguments: ["--random-seed", "1"]``` to barcodecollapse_se and demux_se definitions to decrease randomness in umi_tools outputs
- added an "wf_encode_se_full" and "wf_encode_se_full_scatter" cwl definitions to run 1) peak finding, 2) region level normalization, 3) repeat mapping for SE reads.
- region normalization subworkflow (regionnormalize/) cwl definitions to incorporate region level normalization
- repeat mapping subworkflow (repmap/) cwl definitions to incorporate repeat mapping

### Changed
- makebigwigs script is now split into _PE and _SE due to strand flipping
- repeat-mapped reads now are named dataset.readname.umi.r1.repeat-mapped.bam (instead of dataset.readname.umi.r1TrTr.sorted.STARAligned.out.bam)
- repeat-unmapped reads are now named dataset.readname.umi.r1.repeat-unmapped.sorted.fq (instead of dataset.readname.umi.r1TrTr.sorted.STARUnmapped.out.sorted.fq.gz)
- genome-mapped reads now are named dataset.readname.umi.r1.genome-mapped.bam (instead of dataset.readname.umi.r1TrTr.sorted.STARUnmapped.out.sorted.STARAligned.outSo.rmDupSo.bam)
- wf_trim_and_map_se.cwl now outputs gzipped X_output_trim_first and X_output_trim_again fastq files.

[Unreleased]: https://github.com/yeolab/eclip...HEAD

