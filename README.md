# GNU Octave Fixed-Point (fxp) Data Type

A lightweight fixed-point numeric data type for GNU Octave, implemented as a class (`@fxp/fxp.m`). The library is intended for fixed-point modeling, algorithm validation, and educational use.

## Features

- Signed or unsigned fixed-point formats
- Configurable word-length (WL) and fraction-length (FL)
- Saturation or wrap overflow handling (`ovf_action`)
- Basic rounding method selection (`rnd_method`)
- Overloaded arithmetic operators (`+`, `-`, `*`, `/`, `mod`)
- Overloaded comparison operators (`==`, `~=`, `<`, `<=`, `>`, `>=`)
- Convenience conversion methods (`double`, `int32`, `uint32`, `struct`)
- Readable binary string formatting (`bin_str`)

## Repository Layout

Recommended layout for GNU Octave classes:

```
fxp/
├─ @fxp/
│  └─ fxp.m
├─ testing
|  └─ test_regression.m
|  └─ test_regression_py_compare.m
|  └─ run_fxpmath_ref.py
└─ README.md
```

> Important: In GNU Octave, a class named `fxp` must live in a folder called `@fxp/`.

## Installation

### Option A — Clone

```bash
git clone https://github.com/ahmedshahein/fxp.git fxp
cd fxp
```

Then add the repository root (the folder that contains `@fxp/`) to your Octave path:

```octave
addpath(pwd);
rehash;
```

### Option B — One-shot install script (Linux/macOS)

The snippet below clones the repository into `~/octave/fxp`, then updates your `~/.octaverc` so the class is found automatically.

```bash
#!/bin/bash

PKG_PATH="/home/$USER/octave/fxp"
GIT_PATH="https://github.com/ahmedshahein/fxp.git"

mkdir -p "$PKG_PATH"
git clone "$GIT_PATH" "$PKG_PATH"

cat <<EOF >> /home/$USER/.octaverc
addpath('$PKG_PATH');
rehash;
EOF
```

## Quick Start

Create a fixed-point value using explicit configuration:

```octave
v = fxp(22/7, 1, 16, 8);
disp(v);
```

Use default configuration (currently `S=1`, `WL=16`, `FL=8`) by passing only the data:

```octave
v = fxp(3.14);
```

Enable saturation overflow handling:

```octave
v = fxp(1e9, 1, 16, 8, 'ovf_action', 'sat');
```

Arithmetic is supported for two `fxp` operands:

```octave
a = fxp(1.25, 1, 16, 8);
b = fxp(0.50, 1, 16, 8);

c1 = a + b;
c2 = a - b;
c3 = a * b;
c4 = a / b;
```

## Public API (Main Fields)

After construction, the following fields are commonly useful:

- `vfxp`   — quantized fixed-point value (double)
- `dec`    — scaled integer representation
- `bin`    — binary vector (MSB-first)
- `bin_str`— formatted binary string with radix point
- `err`    — quantization error
- `ovf`    — overflow flag (1 if overflow detected)

Configuration fields:

- `S`, `WL`, `IL`, `FL`
- `ovf_action` (`'sat'` or `'wrap'`)
- `rnd_method` (`'round'`, `'fix'`, `'floor'`, `'ceil'`)

## Notes and Limitations

- The class is intended for modeling; it is not a bit-true hardware simulator unless you explicitly validate rounding and overflow behavior for your target.
- Some methods may assume configuration compatibility between operands (for example, arithmetic methods require the same `ovf_action` and `rnd_method`).
- Binary conversion uses `de2bi`, which is provided by the Communications package in some Octave installations.

## Testing

If the repository includes a regression test, run it from the repository root:

```octave
test_regression
```

## License

See the header of the source file for copyright and licensing details.
