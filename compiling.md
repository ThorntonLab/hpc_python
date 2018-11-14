# Compiling a module using an "env"

Steps are shown using fwdpy11 as an example.

The intent is to install against fwdpy11/dev_015:

## Getting ready

```sh
# Make sure existing C/C++ compilers cannot interfere
module purge
# load lab's conda module
module load krthornt/anaconda
# activate the correct environment
source activate fwdpy11_0_2_0
```

## Example: compiling fwdpy11

The "Gotcha" is that you need to set CPPFLAGS manually, else we cannot find GSL v2.4.

Oddly, there is no need to set LDFLAGS...

```sh
git clone https://github.com/molpopgen/fwdpy11
cd fwdpy11
git checkout dev_015
CPPFLAGS=-I/data/apps/user_contributed_software/krthornt/anaconda3/envs/fwdpy11_0_2_0/include  python setup.py build_ext -i
```

The hope is that you can just use CPPFLAGS for compiling fwdpy11_arg_example, which indeed seems to have worked for my
user, after I fixed an issue that I haven't seen before with fwdpp, which is making operator== inline for a bunch of
types in fwdpp::ts.  I checked your "ancestral_sample" branch.  I've pushed a fix to fwdpp, and will get this into
fwdpy11 and onto HPC ASAP.
