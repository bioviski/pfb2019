Unix Basics Quick Review and Problem Set
======================================

Table of Contents
 * [Quick Review](#quick-review)
 * [Problem Set](#problem-set)

Quick Review
=========================

command | description
-------|------------
ls   | list contents
cd   | change directory
mkdir | make a directory
rm   | use caution, it is easy to delete more that you would like
head  | prints the top few lines to the terminal window
tail  | prints the last few lines to the terminal window
sort  | sorts the lines
uniq  | prints the unique lines
grep  | filnds the lines that contain a pattern
wc  | counts the number of lines, characters and words
mv | move files
cp  | copy files
date | returns the current date and time
pwd  | return working directory name
ssh  | remote login
scp  | remote secure copy
\~    | represents your home directory
man [command] | manual page for the command ex. man ls





__How do these two commands compare?__

Try it!!
```
ls -l
ls -lt
```
<p><br></p>

__Pipes__

You can string more than one command together with a pipe (|) , such that the output of the first command is received by the second command.

Try it!!
```
ls -lt | head
```

<p><br></p>

__Semicolons__

You can string more than one command together with a semi-colon (;) , such that the commands run sequentially, but that output does not get passed into the next command.

Try it!!
```
date ; sleep 2 ; date
```
> If you want to know more about `sleep` use `man sleep`

<p><br></p>

__Redirect STDOUT__  
You can redirect the output of a command into a file

Try it!!
```
grep Chr7 cuffdiff.txt > fav_chr_cuffdiff.txt
```

<p><br></p>

__Redirct STDOUT and Append__

You can append the output of a command to a file

Try it!!
```
grep Chr9 cuffdiff.txt >> fav_chr_cuffdiff.txt
```

<p><br></p>

__Redirect STDERR__  

You can redirect STDERR to a file.

Let's review what STDERR actually is.
```
cat blablabla.txt
```
> file blablabla.txt does not exist so we get `cat: blablabla.txt: No such file or directory` printed to the terminal. This message is labeled by the operating system as an error message or STDERR. 

STDERR is a labeled type of output we can redirect

Try it!!
```
cat blablabla.txt 2> errors.txt
```
> We can redirect the error messages, A.K.A. STDERR, to a new file called anything we want

   
What happens when you try to redirect STDOUT?
```
cat blablabla.txt > errors.txt
```
> `cat: blablabla.txt: No such file or directory` still gets printed to the screen because we only redirect STDOUT to our file. There is no STDOUT in this case and our file will be empty


<p><br></p>

__Redirect STDOUT and STDERR__

You can redirect both STDOUT and STDERR to **TWO SEPARATE** files in one command.
   
Try it!!
```
# just print it to the terminal first
cat fav_chr_cuffdiff.txt blablabla.file

# redirect to two files, STDOUT to out.txt, STDERR to err.txt 
cat fav_chr_cuffdiff.txt blablabla.file > out.txt 2> err.txt
```
> Examine the contents of `out.txt` and `err.txt`

<p><br></p>

You can redirect both STDOUT and STDERR to **ONE SINGLE** file in one command.
```
cat fav_chr_cuffdiff.txt blablabla.file &> all_out_err.txt
```


Problem Set
===========

1. Log into your machine or account. 

2. What is the full path to your home directory?

3. Go up one directory?
        - How many files does it contain?
        - How many directories?

4. If you have not already done so, follow [Steps 1-3 in Unix: GIT for Beginners](https://github.com/srobb1/pfb2017#git-for-beginners). Here is a summary of those steps:
   - Create a GitHub Account and Click New: Create a New Remote Repository
   - Add info about your repository
   - Create a local (your machine) directory (`mkdir`) and repository (`git init`) and link it to your remote repository (`git remote add`).


5. Create a directory call `files` in your ProblemSets directory. 

6. Make a copy of the file `sequences.nt.fa` to your `files` directory

7. ADD/COMMIT/PUSH `sequences.nt.fa` to your remote repository
  - `git add files/sequences.nt.fa`
  - `git commit -m 'adding sequences.nt.fa'`
  - `git push`
  - Visit the your GitHub repository website (on github.com) and see the file from your local repository that you just pushed up to your remote repository.

8. Without using a text editor examine the contents of the file `sequences.nt.fa`.
      - How many lines does this file contain?   
      - How many characters?    (Hint: check out the options of wc)
      - What is the first line of this file?    (Hint: read the man page of head)
      - What are the last 3 lines?    (Hint: read the man page of tail)
      - How many sequences are in the file?    (Hint: use grep)    

6. Rename `sequences.nt.fa` to something more informative like `cancer_genes.fasta`. (Hint: read the man page for mv)

7. ADD/COMMIT/PUSH your new file to your remote repository. Did the file name change on your github.com repository

5. Using your text editor (nano is a good one to start with) create a fasta file and name it `mysequences.fasta`. Make sure it ends up in your problem sets files directory.

This is fasta file format:
```
>seqName description
ATGGCGTCTTGGCCTTAAAAGCTC
``` 

6. ADD/COMMIT/PUSH `sequences.nt.fa` to your remote.



7. Create a directory called fasta.     (Hint: use mkdir)
    8. Copy the fasta file that you renamed to the fasta directory. (Hint: use cp)
    9. Verify that the file is within the fasta directory.    (Hint: use ls fasta/)
    10. Delete the the original file that you used for copying.    (Hint: use rm, be careful)
    11. Read the man page for rm and cp to find out how to remove and copy a directory.
    12. Print out your history and redirect it to a file called unixBasics.history.txt

    13. In /pfbhome/data there is a file called: cuffdiff.txt 
        - the descriptions of each column in the file are below
	- look at the first few lines of the file
	- sort the file by log fold change 'log2(fold_change)', from highest to lowest, and save in a new file in your directory called sorted.cuffdiff.out
  	- sort the file (log fold change highest to lowest) then print out only the first 100 lines. Save in a file called top100.sorted.cuffdiff.out
	- sort the file, print only first column. Get a unique list of the genes, then print only the top 100. Save in a file called differentially.expressed.genes.txt



Cuffdiff file format
--------------------
Column number    Column name       Example           Description
1                Tested id         XLOC_000001       A unique identifier describing the transcipt, gene, primary transcript, or CDS being tested
2                Tested id         XLOC_000001       A unique identifier describing the transcipt, gene, primary transcript, or CDS being tested
3                gene              Lypla1            The gene_name(s) or gene_id(s) being tested
4                locus             chr1:4797771-4835363    Genomic coordinates for easy browsing to the genes or transcripts being tested.
5                sample 1          Liver             Label (or number if no labels provided) of the first sample being tested
6                sample 2          Brain             Label (or number if no labels provided) of the second sample being tested
7                Test status       NOTEST            Can be one of OK (test successful), NOTEST (not enough alignments for testing),
                                                       LOWDATA (too complex or shallowly sequenced), HIDATA (too many fragments in locus), or FAIL,
                                                       when an ill-conditioned covariance matrix or other numerical exception prevents testing.
8                FPKMx             8.01089           FPKM of the gene in sample x
9                FPKMy             8.551545          FPKM of the gene in sample y
10                log2(FPKMy/FPKMx) 0.06531           The (base 2) log of the fold change y/x    
11               test stat         0.860902          The value of the test statistic used to compute significance of the observed change in FPKM
12               p value           0.389292          The uncorrected p-value of the test statistic
13               q value           0.985216          The FDR-adjusted p-value of the test statistic
14               significant       no                Can be either "yes" or "no", depending on whether p is greater then the FDR after
                                                     Benjamini-Hochberg correction for multiple-testing
