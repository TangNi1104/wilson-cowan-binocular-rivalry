# Empirical data (not redistributed)

Obtain authorised behavioural data for Han et al. (2024), *Binocular rivalry under naturalistic geometry: Evidence from worlds simulated in virtual reality*, DOI: 10.1093/pnasnexus/pgae054.

The notebook expects this folder layout:

```text
Data/
  exp 1/
    Motion/<participant folders>/**/*.txt
    Static/<participant folders>/**/*.txt
  exp 2/
    Motion/<participant folders>/**/*.txt
    Static/<participant folders>/**/*.txt
```

Each text file is loaded without a header. Original zero-based columns 3, 5 and 6 are interpreted as percept, time and raw duration. Confirm these assumptions against the source data documentation. Only the first sorted text file in each participant folder is loaded by the supplied code; check practice/trial selection before analysis. Raw datasets and participant-level results are not included.
