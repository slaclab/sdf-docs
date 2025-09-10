# Data transfer

`s3dfdtn.slac.stanford.edu` is a load-balanced DNS name which points
to a pool of dedicated data transfer nodes. It is open to everyone
with an S3DF account. Common tools like scp/sftp/rsync are available
for casual data transfers. For serious large volume data transfer, you
may consider `bbcp` and `globus`.

## bbcp

This is a high performance multi-stream data transfer tool developed
at SLAC. In its simplest form, the `bbcp` command line is similar to
that of `scp`. A simple command using bbcp at SDF looks like this:\
`bbcp me@remote.univ.edu:/tmp/myfile ./myfile`\
You may need to type your password for `me@remote.univ.edu`, unless
you setup password-less login to `remote.univ.edu` (e.g. ssh key).

To achieve high performance, bbcp opens an additional TCP port. This
sometime won't work if there is a firewall.  The `-Z` option allows
you to specify a range of TCP ports that are not blocked by
firewall. The `-z` is another commonly used option to work with
firewall. Type `bbcp --help` or go to the [bbcp web
page](https://www.slac.stanford.edu/~abh/bbcp/) for more info.

Both source and destination must have the bbcp executable in
$PATH. The bbcp executable can be downloaded by following the link in
the bbcp web page. If bbcp is not in `$PATH`, use the `-S` or `-T`
option to specify the non-standard location. Please carefully read the
bbcp web page with regards to these options as they are not as
intuitive as you may think. Also, sometimes a cut-n-paste of dash
(`-`) from the web page end up with something that looks like a dash
but not a dash. In that case, just replace it with a real dash.

Using the above command line as a example, if you copy bbcp to your
home directory at `remote.univ.edu`, enter:\
`bbcp -S 'ssh -l %U %H ~/bbcp' me@remote.univ.edu:/tmp/myfile ./myfile`\
Here we use option `-S` because `remote.univ.edu` is the data
source. bbcp will substitute `%U` and `%H` with `me` and
`remote.univ.edu` respectively.

[More examples from NERSC](https://docs.nersc.gov/services/bbcp/). You
can find more information at the [bbcp
page](https://www.slac.stanford.edu/~abh/bbcp/).

## Globus

S3DF has a Globus 5 testing endpoint `slac#s3df_globus5`. This service is 
available to everyone with an S3DF account. You can find more information
at the [Globus page](https://www.globus.org).

## Trouble shooting

A common issue with data transfer is that "it is slow". The performance 
of the wide area network data tranfers involves the SLAC storage, the 
storage at the other side, and the network in between. 

### Checking the storage

The following example assumes a posix storage. The storage at both ends
should be checked:

    - dd if=/dev/zero of=$HOME/zeros bs=2k count=65536 oflag=direct
    - dd if=$HOME/zeros of=/dev/null bs=2k iflag=direct

At SLAC, this can be done on a data transfer node (s3dfdtn.slac.stanford.edu).
The speed of the write/read from the above commands aren't the very important
(as long as they are not below single MB/s range). The change overtime is
important (indicating potential problems).

### Checking the WAN (wide area network)

SLAC DTNs have `iperf3` installed. One can run an `iperf3` server/client at 
the SLAC DTN and run `iperf3` client/server at the other end. This will give
an estimation of expected network performance.
