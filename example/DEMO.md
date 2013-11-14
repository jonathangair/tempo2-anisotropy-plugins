# Sample GWanisobkgrd harmfile and pre-injection TOAs #

## Harmfile ##

The harmfile contains an integer on the first line which specifies the number of harmonics in the file.

Each subsequent line specifies the value of "l", "m", and the amplitude for the harmonic relative to the isotropic component.

For example, in SampleHarmfilePureQuad we have two harmonics, so the integer "2" is placed on the first line. We then specify the isotropic component via `0 0 1.0` for `l=0`, `m=0` and the relative amplitude being "1.0" by definition. For the second harmonic we inject maximal quadrupole with `l=2`, `m=0`. The amplitude of this harmonic will be 4*\sqrt(PI/5), so the relative amplitude written in our harmfile is this amplitude divided by 2*\sqrt(PI), i.e. 2*\sqrt(1/5) = 0.8944272.

The following block can be copied directly to a file and used as input to the GWanisobkgrd plugin. It will produce a maximal-quadrupole anisotropy. **Note that the first line is a list of the number of harmonics, not the maximum `l`.** 

```
2
0 0 1.0
2 0 0 0.8944272
```

## Sample TOAs ##

The SampleParTim directory contains sample pulsar parameter and timing files. The timing files contain 5 years of fortnightly observations, with white-noise set by 100 ns TOA error-bars.