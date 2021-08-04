# Data transfer

`sdf-dtn01.slac.stanford.edu` is a dedicate data trasnfer node. It is open to everyone with a SDF account. 
Common tools/service like scp/sftp/rsync are
available for casual data transfer. For serious large volume data transfer, two common services are available:
`bbcp` and `Globus`.

## [bbcp](https://www.slac.stanford.edu/~abh/bbcp/)

bbcp is a high performance multi-stream data transfer tool. In its simplest form, the `bbcp` command line is
similar to that of `scp`. A simple command using bbcp at SDF looks like this:
```
bbcp me@remote.univ.edu:/tmp/myfile ./myfile
```
You may need to type your password for `me@remote.univ.edu`, unless you setup password less login to 
`remote.univ.edu` (e.g. ssh key).

To archive high performance, bbcp opens a additional TCP port. This sometime won't work if there is a firewall. 
The `-Z` option allows you to specify a range of TCP ports that are not blocked by firewall.  
The `-z` is another commonly used option to work with firewall. 
Type `bbcp --help` or go to the bbcp web page for more info.

Both source and destination must have the bbcp executable in $PATH. bbcp executable can be downloaded
by following the link in the bbcp web page. If bbcp is not in `$PATH`, use the `-S` or `-T` option to 
specify the none standard location. Please carefully read the bbcp web page with regards to these options as they 
are not as intuitive as you may think. Also, sometimes a cut-n-paste of dash (`-`) from the web page end up with
something that looks like a dash but not a dash. In that case, just replace it by a real dash. 

Using the above command line example, if you copy bbcp to your home director at `remote.univ.edu`, do this:
```
bbcp -S 'ssh -l %U %H ~/bbcp' me@remote.univ.edu:/tmp/myfile ./myfile
```
Here we use option `-S` because `remote.univ.edu` is the data source. bbcp will substitute `%U` and `%H` by 
`me` and `remote.univ.edu` respectively.

More [examples from NERSC](https://docs.nersc.gov/services/bbcp/).

## [Globus](https://www.globus.org)

SDF has a Globus endpoint `slac#sdf`. This service is available to everyone with a SDF account.

