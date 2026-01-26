# fxp — Fixed-point (fxp) data type for GNU Octave

This package provides the `fxp` class: a fixed-point data type intended for
algorithm exploration and verification (e.g., DSP pipelines) inside GNU Octave.

## Quick start

```octave
pkg install fxp-1.0.0.tar.gz
pkg load fxp

x = fxp([0:0.1:8], 0, 10, 7);
y = fxp([0:0.2:16], 0, 12, 8);
z = x + y;
disp(z);
```

## Package layout

- `inst/@fxp/fxp.m`: the class implementation (installed onto the Octave path)
- `doc/fxp.texi`: package documentation (installed for reference)
- `DESCRIPTION`, `COPYING`, `INDEX`, `NEWS`: package metadata for Octave's `pkg`

## License

GPL-3.0-or-later. See `COPYING`.
