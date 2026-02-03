# MacPorts Notes & Cheatsheet

Quick reference for **MacPorts** commands, workflows, and common tricks on macOS.
Focused on day-to-day usage, compiler management (GCC / gfortran), and avoiding common pitfalls.

---

## Basics

Update MacPorts

```
bash
sudo port selfupdate
```

Search for a port

```
port search <name>
port info <name>
```

Install a port

```
sudo port install <portname>
```

Uninstall a port

```
sudo port uninstall <portname>
```

## Upgrading & Maintenance

Upgrade outdated ports

```
sudo port upgrade outdated
```

List outdated ports

```
port outdated
```

Clean old build files

```
sudo port clean --all <portname>
```

Remove inactive ports

```
sudo port uninstall inactive
```

## GCC & gfortran (important)

MacPorts installs versioned compilers to allow multiple versions to coexist.
Install GCC (includes gfortran)

```
sudo port install gcc13
```

This provides:

    gcc-mp-13

    g++-mp-13

    gfortran-mp-13

Check version

```
gfortran-mp-13 --version
```

Select default GCC / gfortran

```
sudo port install gcc_select
sudo port select --set gcc mp-gcc13
```

Verify:

```
gfortran --version
gcc --version
```

Use a specific compiler without selecting

```
gfortran-mp-13 program.f90
```

## Variants

Ports often support variants (optional features).

Show available variants

```
port variants <portname>
```

Install with variants

```
sudo port install <portname> +variant1 -variant2
```

Example:

```
sudo port install openmpi +fortran
```

## Diagnostics & Troubleshooting

See why a port is installed

```
port dependents <portname>
```

Show dependencies of a port

```
port deps <portname>
```

Check active versions

```
port installed
```

Get verbose build output

```
sudo port install <portname> -v
```

## Common Pitfalls

    Do not mix Homebrew and MacPorts compilers or libraries in the same build

    Always install Xcode Command Line Tools:

    xcode-select --install

    Prefer versioned compiler names (gfortran-mp-13) in scripts for reproducibility

    Use port select only when you want a global default

## Useful Tips

Find where a port installed files

```
port contents <portname>
```

Show Portfile (build instructions)

```
port cat <portname>
```

Dry-run an install

```
port install <portname> --pretend
```
