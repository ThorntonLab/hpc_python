# Running jobs

To run a job using fwdpy11 0.2.x.

SGE commands take a #$ to distinguish them from comments.  Otherwise, a job is a fairly normal bash script.

```sh
#!/bin/bash

# Submit to AMD EPYC queue
# and fast Intel queue
#$ -q krt2, krti
# Request a range of cores.
# Will assign obtained value to 
# shell variable CORES
#$ -pe openmp 64-128

cd $SGE_O_WORKDIR
module load krthornt/anaconda
source activate fwdpy11_0_2_0

PYTHONPATH=$HOME/src/fwdpy11_arg_example python ~/src/fwdpy11_arg_example/mysim.py --ncores $CORES
```

To submit:

```
qsub script.sh -N jobname
```

The `-N jobname` bit is optional.

You can/should create your scripts in the partition /share/kevin2/dlawrie, and submit them *from there*.  Doing this
means that all the I/O is going to that partition, which is ours.  If you make jobs scripts in, and submit from, ~/, 
then you are working in your user's folder which is a.) very small with limited quota and, b.) too slow.
