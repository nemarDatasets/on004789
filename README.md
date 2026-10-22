[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.on004789-blue)](https://doi.org/10.82901/nemar.on004789)

### Delayed Free Recall of Word Lists

#### Description
This dataset contains behavioral events and intracranial electrophysiological recordings from a delayed free recall task.  The experiment consists of participants studying a list of words, presented visually one at a time, completing simple arithmetic problems that function as a distractor, and then freely recalling the words from the just-presented list in any order.  The data was collected at clinical sites across the country as part of a collaboration with the Computational Memory Lab at the University of Pennsylvania.

#### To Note
* The iEEG recordings are labeled either "monopolar" or "bipolar."  The monopolar recordings are referenced (typically a mastoid reference), but should always be re-referenced before analysis.  The bipolar recordings are referenced according to a paired scheme indicated by the accompanying bipolar channels tables.
* Each subject has a unique montage of electrode locations.  MNI and Talairach coordinates are provided when available, along with brain region annotations.
* Recordings were made on multiple different systems, so we have done the scaling to provide all voltage values in V.

#### Contact
For questions or inquiries, please contact sas-kahana-sysadmin@sas.upenn.edu.

## Channel names follow the data headers (18 Oct 2026)

In 12 recordings the channel list of channels.tsv did not equal the data-file header (names, order or count). In the 12 with a different channel count, `mne_bids.read_raw_bids` warned and kept the header names, so the channels.tsv types and bad-channel status reached only the channels whose names happen to be identical; a reader that applies the channels.tsv rows by position gives wrong labels wherever the two lists are not aligned. Since 18 Oct 2026 every channels.tsv lists exactly the header channels, in header order, with the header names (MNE names: duplicated header labels numbered -0, -1).

Rows were matched to header channels BY NAME, never by position (exact; then case/whitespace; then the recorder prefix 'EEG '/'POL ', '_' and zero padding; then a trailing '-<reference>' token). Matched rows keep all their columns (type, units, status, ...); 0 rows took the header name.

101 channels.tsv rows had no channel in the data file (12 files) and were removed; they are kept verbatim under `sourcedata/channels-removed-2026-10-18/` (same relative path). Examples: `sub-R1350D_ses-0_task-FR1_acq-bipolar_ieeg.edf`: LAHCMD2-LAHCMD3, LAHCMD4-LAHCMD5, LAHCMD6-LAHCMD7, LAHCMD8-LAHCMD1, LPHCMD2-LPHCMD3; `sub-R1350D_ses-1_task-FR1_acq-bipolar_ieeg.edf`: LAHCMD2-LAHCMD3, LAHCMD4-LAHCMD5, LAHCMD6-LAHCMD7, LAHCMD8-LAHCMD1, LPHCMD2-LPHCMD3; `sub-R1350D_ses-2_task-FR1_acq-bipolar_ieeg.edf`: LAHCMD2-LAHCMD3, LAHCMD4-LAHCMD5, LAHCMD6-LAHCMD7, LAHCMD8-LAHCMD1, LPHCMD2-LPHCMD3.

Applied by position, the former rows would have given wrong labels to 560 channels in 10 files (rows missing, extra or out of order before that position).
