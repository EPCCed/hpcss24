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
you want to explore things a bit more you can work on applying the
morning's HPC techniques to two examples: one based on image
processing, the other a simple computational fluid dynamics example.

## Material

### Monday AM

We will use Carpentries material for this session. See:

  * HPC Carpentry Day 1 https://epcced.github.io/2024-06-19-hpc-shell-shampton/
  * Introduction to git https://swcarpentry.github.io/git-novice/

The HPC Carpentry material was run by EPCC very recently for a course
on the national ARCHER2 supercomputer. We will be using a different
HPC system at EPCC, Cirrus, but all you have to do is replace
occurrences of "ARCHER2" with "Cirrus"!

### Monday PM

Here is the [claims form](docs/student_and_non_staff_expenses_claim_form.docx)

You can find the image sharpening example at
https://github.com/EPCCed/hpcss24-sharpen

I will explain this program and how it works on Wednesday but for now
we'll just be using the Python serial version in the `P-SER` directory
as an example of a program that does lots of computation.

On Cirrus you will need to load a module to get a suitable version of Python: `module load python/3.9.13`

To view the input and output images (`fuzzy.pgm` and `sharpened.pgm`),
use `module load ImageMagick` then `display image.pgm`.

Things you might like to investigate:

  * How fast is the code on your laptop compared to the Cirrus login nodes?

  * If you want the program to run faster you can change the size of
  the smoothing filter - try reducing the value of `d` in
  `sharpenalg.py` from its default value `d=8`. How does the runtime
  vary with `d`? Can you understand this behaviour by looking at the
  code?

  * The program is deliberately written very simply and the
    performance can easily be improved. For example, the values of the
    (very time-consuming) function `filter()` could be pre-calculate
    and stored in an array. If you do alter the code make sure that
    the output is still correct, e.g. by comparing the output image
    `sharpened.pgm`.

### Tuesday AM

  Ludovic will distribute his slides covering an Introduction to C

### Tuesday PM

  As well as the pagerank example, you can look at the C version of
  the Image Sharpening code in `C-SER`.

  The exercise is described in `doc/sharpen-cirrus1.pdf` - the
  material up to and including section 3.8 is relevant here.

  Things to look at include:

  * How much faster is the compiled C version compared to the Python code?
  * Does adding compiler optimisation (e.g. `-O3`) change the performance?
  * Does using the GNU compiler `gcc`, as opposed to Intel's `icc`,
    change things?

### Wednesday AM

  * Go to https://b.socrative.com/login/student/
  * "Room" is HPCQUIZ

  Here are the slides for the Introduction to HPC:

  * [Why HPC](slides/L01_WhyHPC.pdf)
  * [Image Sharpening](slides/L02_Sharpen.pdf)
  * [Parallel Programming](slides/L03_ParallelProgramming.pdf)
  * [Hardware](slides/L04_CPUMemAcc.pdf)
  * [Parallel Programming Models](slides/L07_ParallelModels.pdf)


  You should work through the Image Sharpening worksheet and look at
  the performance and parallel scalability of the code.

  To see the code and exercise sheets, go to [https://github.com/EPCCed/hpcss24-sharpen](https://github.com/EPCCed/hpcss24-sharpen)

  To get these onto Cirrus just use:

    git clone https://github.com/EPCCed/hpcss24-sharpen

We have a reservation of 8 nodes for fast turnaround all day today. To use this:

````
    #SBATCH --qos=reservation
    #SBATCH --reservation=tc063_Q2482854
````
    

### Wednesday PM

 There are also OpenMP and (serial) Python versions that you could look at.

   * How does the scalability of the OpenMP code (using threads not processes) compare to MPI?
   * How does using OpenMP limit the ultimate speed of the program compare to MPI?

### Thursday AM

  Ludovic will distribute his slides covering an Introduction to OpenMP

### Thursday PM

  You are welcome to continue with Ludovic's OpenMP
  exercises. However, if you want to tackle something different see
  below:

  You should work through the CFD worksheet and look at the
  performance and parallel scalability of the code.

  To see the code and exercise sheets, go to [https://github.com/EPCCed/hpcss24-cfd](https://github.com/EPCCed/hpcss24-cfd)

  To get these onto Cirrus just use:

    git clone https://github.com/EPCCed/hpcss24-cfd

  The exercise sheet only covers the serial and MPI versions of the
  cfd example. Here are some things you could consider with the serial
  Python and parallel OpenMP versions. When compiling code I would
  recommend using the `-O3` optimisation level.


  * Visualising the Python output requires you to run an additional
    program: ` python ./plot_flow.py velocity.dat colourmap.dat
    output.png`. You can then view the PNG file with `display`.
  * How long does the Python code take compared to the serial C code
    (consider a small example for a reasonable runtime)?
* Is the performance different on the login vs compute nodes (you will
    need to write an appropriate Slurm script). What about the serial
    C code?
* There is a version that uses numpy arrays and array syntax rather
    than lists and explicit loops - see `cfd_numpy` and
    `jacobi_numpy`. How much faster is this than the basic Python
    code? Do you understand why? Again, is there a performance difference between login and compute nodes?

* Try running the OpenMP code - how does its performance scale with
  varying values of `OMP_NUM_THREADS`. For large values you must run
  on the compute nodes - again, you will need to write a Slurm
  script. How does this compare to MPI? Do you seen any unusual
  effects when the thread count exceeds 18 - can you explain this?

* How does the OpenMP performance scaling compare between the default
  parameters and running with a finite value of the Reynolds number,
  e.g. 2.0? Can you see what the problem is? Can you fix it by adding
  appropriate OpenMP directives?

### Friday AM

  Ludovic will continue his OpenMP workshop

### Friday PM

  The way that `dosharpen` is parallelised in OpenMP is a bit weird - it is done by hand and does not use `parallel for`.

  Rewrite the code so it uses `parallel for` over the first loop
  rather than switching based on the value of `pixcount`. Is the
  performance similar to the original version? What loop schedule
  should you use - does it make a difference to performance?

  [Here is a version of `dosharpen`](docs/dosharpen.c) written
  deliberately to have load imbalance within the main loop (the width
  of the filter is varied across the image from `2` to `d`). As
  above, rewrite the code to use `parallel for`. Does the loop
  schedule affect performance for the load-imbalanced sharpening
  algorithm?  What is the best schedule - `static`, `dynamic`. ... ?

### Monday AM

  Ludovic will distribute slide for his OpenMP GPU offload workshop

### Monday PM

  There is a lot to learn for GPU offload so please continue with
  exercises from this morning, but I have added a "C-GPU" directory to
  the hpcss24-cfd git repo which contains a simple example of using
  these directives for the cfd example.

  As for the previous OpenMP example the code only currently works for
  the simpler case when you do not specify a Reynolds number (i.e. for
  inviscid / irrotational flow). If you want you can try to extend to
  the general case.

  When measuring performance you will need to run much larger problems
  than for the CPU as you need a lot of grid points to keep the very
  large number of GPU threads active. You will also need to run for a
  large number of iterations to get reliable performance results: for
  large problems the cost of copying data to and from the GPU can be
  significant.

  The reservation for today is `tc063_1270277`