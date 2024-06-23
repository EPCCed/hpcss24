# EPCC HPC Summer School 2024

For the HPC Summer School we're using material from a range of
existing courses so this is a central page to help collect them all
together.

## Schedule

| Day | Morning | Afternoon |
| --- | ---  | --- |
| |  | |
| Mon 24 | Bash shell / git | Familiarisation / Python image sharpening |
| Tue 25 | Introduction to C | C image sharpening |
| Wed 26 | Introduction to HPC | Parallel image sharpening |
| Thu 27 | OpenMP for CPUs (i) | Parallel CFD example |
| Fri 28 | OpenMP for CPUs (ii) | Parallel CFD example |
| | | |
| Mon 1 | OpenMP for GPUs (i) | Parallel CFD example |
| Tue 2 | OpenMP for GPUs (i) | Parallel CFD example |
| Wed 3 | Introduction to MPI (i) | Parallel CFD example |
| Thu 4 | Introduction to MPI (ii) | ACF Visit |
| Fri 5 | HPC Guest Lectures | Finish up exercises |

## Overview

The morning lectures will all have associated practicals. You are
welcome to continue working on these in the afternoons, but in case
you want to explore thinsg a bit more you can work on applying the
morning's HCC techniques to two examples: one based on image
processing, the other a simple computational fluid dynamics example.

## Material

### Monday AM

We will use Carpentries material for this session. See:

  * HPC Carpentry Day 1 https://epcced.github.io/2024-06-19-hpc-shell-shampton/
  * Introduction to git https://swcarpentry.github.io/git-novice/

The HPC Carpentry material was run by EPCC very recently for a course
on the national ARCHER2 supercomputer. We will be using a different
HPC system at EPCC, Cirrus, but all you have to do is replace
occurences of "ARCHER2" with "Cirrus"!

### Monday PM

You can find the image sharpening example at
https://github.com/EPCCed/hpcss24-sharpen

I will explain this program and how it works on Wednesday but for now
we'll just be using the Python serial version in the P-SER directory
as an example of a program that does lots of computation.

On Cirrus you will need to load a module to get a suitable version of Python: `module load python/3.9.13`