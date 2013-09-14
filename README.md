=========================
tempo2-anisotropy-plugins
=========================

Plugins for Tempo2 to generate anisotropic GW backgrounds with arbitrary polarisation.

REQUIREMENTS
-------------

You will require a working installation of Tempo2 before installing this software.

INSTALLATION
-------------

Unpack GWAnisoPluginTarball.tar.gz in the main tempo2 directory,

`gtar xzf GWAnisoPluginTarball.tar.gz`

This compressed tar comes with modified plugin Makefiles. Make sure you are still in the main Tempo2 directory. Running,

     make plugins
     make plugins install

should be sufficient, however if the anisotropy plugins were not made then run,

     make
     make install
     make plugins
     make plugins install

If you still have problems, then install Tempo2 from scratch by executing `./configure` before the first `make` command.

THE PLUGINS
------------

There are 6 different plugins included in this repository, which generate GW backgrounds of different types, as described in the following.

### GWbkgrd_plug.C ###

This is the usual GWbkgrd plugin that comes packaged with a Tempo2 download. The user can inject an isotropic stochastic gravitational-wave background signal into model TOAs by specifying the amplitude and slope of the characteristic strain-spectrum of the background.

The polarisation of the GWs is the usual general relativistic transverse tracless modes.

Example usage:

     ./tempo2 -gr GWbkgrd -f psr.par psr.tim -dist 1 -gwamp 1e-15 -alpha -0.666666 -ngw 10000 -plot

### GWbkgrdfromfile_plug.C ###

This plugin allows the user to simulate a gravitational wave background comprised of a set of sources listed in an input file.

Notable command-line options are,

- "GenBkgrdFile" : specify a background file containing constitutent source parameters. We assume these are general sources which may have non-GR polarisation modes.
- "GRBkgrdFile" : specify a background file containing constituent source parameters. We assume these are GR sources with only plus and cross polarisation modes.
- "bkgrdId" : specify a realisation label for the background in the user-supplied file.

Example usage:

     ./tempo2 -gr GWbkgrdfromfile -f psr.par psr.tim -dist 1 -plot -GRBkgrdFile BkrdFileGR.bin

### GWdipolebkgrd_plug.C ###

This plugin allows the user to simulate a gravitational wave background with a dipole anisotropy in a user-specified direction.

Notable command-line options are,

- "dipoleamp a b c" : where a,b,c are the dipole amplitudes for the spherical-harmonic functions Y_1^1 (Y_1^1+Y_1^-1) and (Y_1^1-Y_1^-1) respectively. Note that the magnitude a^2+b^2+c^2 must be less than 1.
- "dipoledir theta phi" : to specify the direction of the dipole anisotropy in spherical coordinates.
- "dipolemag" : specifies the magnitude of the dipole relative to the isotropic component - must be between 0 and 1.
- "writebkgrd bkgrdfile.dat" : write the parameters of the sources constituting the generated background out to the file 'bkgrdfile.dat'.
- "writebkgrdid I" : if specified, uses integer I to identify the background realisation in the output file. Default is 0 if unspecified.

Example usage:

     ./tempo2 -gr GWdipolebkgrd -f psr.par psr.tim -dist 1 -gwamp 1e-15 -alpha -0.666666 -dipolemag 1. -dipoledir 0. 0. -ngw 10000 -plot

### GWgeneralbkgrd_plug.C ###

This plugin allows the user to simulate an isotropic gravitational wave background comprised of arbitrary polarization states.

Notable command-line options are,

- "alphaTT" : GW transverse tensor spectral exponent (usually -0.666) 
- "alphaST" : GW transverse scalar spectral exponent (usually -0.666) 
- "alphaSL" : GW longitudinal scalar spectral exponent (usually -0.666)
- "-alphaVL" : GW longitudinal vector spectral exponent (usually -0.666)
- "gwampTT" : GW transverse tensor amplitude in dimensionless units
- "gwampST" : GW transverse scalar amplitude in dimensionless units
- "gwampSL" : GW longitudinal scalar amplitude in dimensionless units
- "gwampVL" : GW longitudinal vector amplitude in dimensionless units
- "writebkgrd bkgrdfile.dat" : write the parameters of the sources constituting the generated background out to the file 'bkgrdfile.dat'.
- "writebkgrdid I" : if specified, uses integer I to identify the background realisation in the output file. Default is 0 if unspecified.

Example usage:

     ./tempo2 -gr GWgeneralbkgrd -f psr.par psr.tim -dist 1 -gwampTT 1e-15 -alphaTT -0.666666 -gwampST 1e-15 -alphaST -0.666666 -gwampSL 1e-15 -alphaSL -0.666666 -gwampVL 1e-15 -alphaVL -0.666666 -ngw 1000 -plot

### GWanisobkgrd_plug.C ###

This plugin allows the user to simulate an anisotropic gravitational wave background with the usual GR polarisation states.

Notable command-line options are,

- "harmfile" : input file containing a list of harmonics - l m amp - to include in background.
- "writebkgrd bkgrdfile.dat" : write the parameters of the sources constituting the generated background out to the file 'bkgrdfile.dat'.
- "writebkgrdid I" : if specified, uses integer I to identify the background realisation in the output file. Default is 0 if unspecified.

Example usage:

     ./tempo2 -gr GWanisobkgrd -f tt.par 0437.2048.tim -dist 1 -gwamp 1e-15 -alpha -0.666666 -harmfile BkgrdHarmonics -ngw 1000 -plot

### GWgeneralanisobkgrd_plug.C ###

This plugin allows the user to simulate an anisotropic gravitational wave background composed of arbitrary polarisation states.

Notable command-line options are,

- "alphaTT" : GW transverse tensor spectral exponent (usually -0.666) 
- "alphaST" : GW transverse scalar spectral exponent (usually -0.666) 
- "alphaSL" : GW longitudinal scalar spectral exponent (usually -0.666)
- "-alphaVL" : GW longitudinal vector spectral exponent (usually -0.666)
- "gwampTT" : GW transverse tensor amplitude in dimensionless units
- "gwampST" : GW transverse scalar amplitude in dimensionless units
- "gwampSL" : GW longitudinal scalar amplitude in dimensionless units
- "gwampVL" : GW longitudinal vector amplitude in dimensionless units
- "harmfileTT" : input file containing list of harmonics for transverse tensor background - l m amp - to include in background.
- "harmfileST" : input file containing list of harmonics for transverse scalar background.
- "harmfileSL" : input file containing list of harmonics for longitudinal scalar background.
- "harmfileVL" : input file containing list of harmonics for longitudinal vector background.
- "writebkgrd bkgrdfile.dat" : write the parameters of the sources constituting the generated background out to the file 'bkgrdfile.dat'.
- "writebkgrdid I" : if specified, uses integer I to identify the background realisation in the output file. Default is 0 if unspecified.

Example usage: 

     ./tempo2 -gr GWgeneralanisobkgrd -f psr.par psr.tim -dist 1 -gwampTT 1e-15 -alphaTT -0.666666 -harmfileTT TTBkgrdHarmonics -gwampST 1e-15 -alphaST -0.666666 -harmfileST STBkgrdHarmonics -gwampSL 1e-15 -alphaSL -0.666666 -harmfileSL SLBkgrdHarmonics -gwampVL 1e-15 -alphaVL -0.66666 -harmfileVL VLBkgrdHarmonics -ngw 1000 -plot