# findminstep
A Python script to find the optimal step within a failed Gaussian geometry optimization, to use as an initial geometry for a revised input file

`findminstep` is designed to analyze **<a href="https://gaussian.com/input">Gaussian</a> output files (`.out`)** from geometry optimization and `SCRF=ExternalIteration` calculations. 

It does the following:

* extracts energy and convergence criteria step-by-step,
* **detects optimization going in cycle/loop** and excludes such regions from its search for best step,
* recommends the best optimization step(s) based on energy, force/displacement criteria, and moving averages.

---

## Features

* **Multi-Job & Multi-File Support**: Parses individual sub-jobs within a single Gaussian file or processes multiple output files sequentially.

* **Adaptive Terminal Table Display**: Formats and scales output step tables automatically according to terminal window width.
---

## Requirements
**Python**: Compatible with Python 2.7+ and Python 3.x.

**Dependencies** *(optional)*:
* `natsort`: For natural numerical sorting of multi-file command-line arguments.

---

## Usage

```bash
findminstep [options] filename [filename2 filename3 ...]

```

### Options

| Flag | Long Option | Description |
| --- | --- | --- |
| `-h` | `--help` | Display usage information and exit. |
| `-j INT` | `--job=INT` | Select a specific job step number within a multi-job file. |
| `-s` | `--steps` | Print a detailed table of all optimization steps. |
| `-b` | `--beststeps` | Print steps deemed best across individual criteria. |
| `-i INT` | `--strictness=INT` | Set cycling detection strictness (smaller = stricter, default = `3`). |
| `-n INT` | `--normalize-to=INT` | Normalize criteria to `1` (Normal), `2` (Tight), or `3` (VeryTight). |
| `-x` | `--scpcm` | Find the best step for SC-PCM reaction field convergence. |
| `-v` | `--verbose` | Output all steps (alias for `-s`). |

---

## Usage Examples

### 1. Simple Optimization Analysis

Run against a standard Gaussian output file to get the recommended step:

```bash
findminstep calculation.out

```

### 2. Print Detailed Table of All Steps

Display all step energies, forces, displacements, and calculated moving averages:

```bash
findminstep -s calculation.out

```

### 3. Display Best Steps Across All Criteria

Compare steps recommended individually by Energy, Max Force, RMS Force, Max Displacement, RMS Displacement, and Moving Average:

```bash
findminstep -b calculation.out

```

### 4. Process Multi-Job Output Files

Select job 2 from a sequential multi-job output file:

```bash
findminstep -j 2 multi_job.out

```

### 5. SC-PCM Optimization Analysis

Analyze an SC-PCM reaction field calculation:

```bash
findminstep -x scpcm_job.out

```
