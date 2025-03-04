# Proc::ProcessTable

[![Build Status](https://travis-ci.org/mjeveritt/perl-proc-processtable.svg?branch=master)](https://travis-ci.org/mjeveritt/perl-proc-processtable) [![Coverage Status](https://coveralls.io/repos/github/mjeveritt/perl-proc-processtable/badge.svg?branch=master)](https://coveralls.io/github/mjeveritt/perl-proc-processtable?branch=master)

Please use github or [rt.cpan.org](https://rt.cpan.org/Public/Dist/Display.html?Name=Proc-ProcessTable) to submit bugs and patches.

## MAINTENANCE STATUS

This module is maintained by Joachim Bargsten. I have nearly zero knowledge of
the implementation within but wanted to rescue the distribution from
abandonment and try to get critical bug fixes out. This will need to be
a community effort.

The source is in github -

    https://github.com/jwbargsten/perl-proc-processtable

Commit bits will be generously granted, send me your github id.

## STATUS

This is BETA software; it seems to work, but use at your own risk :)

Currently works on darwin, nonstop-ux, Windows (both native MSWin32 and Cygwin), linux,
solaris, aix, hpux, freebsd, irix, dec_osf, bsdi, netbsd, unixware 7.x,
SunOS and openbsd. Please see the "README.osname" files for details on
individual os implementations. Please see the file PORTING if you are
interested in making it work on something else. Please see the file
TODO for a list of issues that need to be addressed (and send me
patches!).

Please note that the Windows port is derived from Cygwin code and is therefore covered
by the Cygwin license (http://cygwin.com/licensing.html).

Multithread support is now available for Solaris; please see
README.solaris for info. It may work under other OS's as well; please
let me know if it does.

Comments, bug reports, patches and especially ports are greatly
appreciated. If you want to submit a patch, *please* use standard
context-diff format; if you're submitting a port, a tarball of the new
files is great.

## DESCRIPTION

This module is a first crack at providing a consistent interface to
Unix (and maybe other multitasking OS's) process table information.
The impetus for this came about with my frustration at having to parse
the output of various systems' ps commands to check whether specific
processes were running on different boxes at a larged mixed Unix site.
The output format of ps was different on each OS, and sometimes
changed with each new release of an OS. Also, running a ps subprocess
from within a perl or shell script and parsing the output was not a
very efficient or aesthetic way to do things.

With this module, you can do things like this:

    # kill memory pigs
    use Proc::ProcessTable;

    my $t = Proc::ProcessTable->new;
    foreach my $p ( @{$t->table} ) {
        if( $p->pctmem > 95 ){
	        $p->kill(9);
        }
    }

There is another short example in the file "example.pl" in the
distribution. For a more elaborate example (in German), see
<http://www.linux-magazin.de/ausgabe.1999.02/Proc/proc.html>.
<shameless plug> If you can't read German, try my other module,
WWW::Babelfish!</shameless plug>

There are also two contributed modules: a module called Proc::Killall
contributed by Aaron Sherman to kill all processes whose command-lines
match a given pattern, and a module called Proc::Killfam by Stephen
Lidie to kill a list of processes and their children. These modules
are installed along with Proc::ProcessTable. Pod documentation is
included in both of them.


## INSTALLATION

This module needs the File::Find and Storable modules in order to
work. File::Find is generally included with perl distributions;
Storable is available from CPAN.

After unpacking the tar file, do:

        perl Makefile.PL
        make
        make test
        make install

There is embedded POD documentation in ProcessTable.pm and
Process/Process.pm.

## ACKNOWLEDGEMENTS

Thanks to the many people who have sent in ports and patches. Without
them this module would be impossible to support on so many platforms.
Patches are noted in the Changes file.

* David Paquet <David.Paquet@cnes.fr>: AIX port
* Mike Romberg <romberg@fsl.noaa.gov>: HPUX port
* Slaven Rezic <eserte@cs.tu-berlin.de>: FreeBSD port
* W. Phillip Moore <wpm@ms.com>: IRIX port
* Peter ? <hooft@natlab.research.philips.com>: IRIX version patch
* Bernhard Schmalhofer <Bernhard.Schmalhofer@gmx.de>: dec_osf port
* Sean Eskins <sean@gilasoft.com>: bsdi port
* Peter Reich <pr@alles.prima.de>: netbsd port
* Aaron Sherman <ajs@ajs.com>: Proc::Killall module
* Steve Lidie <sol0@Lehigh.EDU>: Killfam.pm module
* Martin Lucina <mato@catalyst.net.nz>: Unixware 7.x port
* Shawn Clifford <shawn.a.clifford@lmco.com> SunOS port
* J Robert Ray <jrray@jrray.org>:Windows (Cygwin) port.
* Tom Wyant <twyant3@comcast.net>:Darwin port.
* Mike Steinert <mike.steinert@motorola.com>: Nonstop-UX port.
* <bsd@openbsd.rutgers.edu>: Openbsd port.

Please note that Bernard Schmalhofer is no longer able to provide
support for the dec_osf port.

## COPYRIGHT

Copyright (c) 1998-2008 Daniel J. Urist. All rights reserved.
This package is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.
