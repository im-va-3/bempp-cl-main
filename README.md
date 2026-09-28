# Bempp-cl
[![Documentation Status](https://readthedocs.org/projects/bempp-cl/badge/?version=latest)](https://bempp-cl.readthedocs.io/en/latest/?badge=latest)
[![DOI](https://joss.theoj.org/papers/10.21105/joss.02879/status.svg)](https://doi.org/10.21105/joss.02879)

Bempp-cl is an open-source boundary element method library that can be used to assemble all the standard integral kernels for
Laplace, Helmholtz, modified Helmholtz, and Maxwell problems. The library has a user-friendly Python interface that allows the
user to use BEM to solve a variety of problems, including problems in electrostatics, acoustics and electromagnetics.

Bempp-cl began life as BEM++, and was a Python library with a C++ computational core. The ++ slowly changed into pp as
functionality gradually moved from C++ to Python with only a few core routines remaining in C++. Bempp-cl is the culmination
of efforts to fully move to Python. It is an almost complete rewrite of Bempp: the C++ core has been replaced by highly SIMD
optimised just-in-time compiled OpenCL kernels, or alternatively, by just-in-time compiled Numba routines, which are
automatically used on systems that do not provide OpenCL drivers. User visible functionality is strictly separated from the
implementation of computational routines, making it easy to add other discretisation technologies in the future (e.g. future
support for SYCL-based heterogeneous compute devices).

## Installation
Bempp-cl can be installed from this repository by running:
```bash
python -m pip install .
```

Full installation instuctions, including installation of dependencies, can be found at
[bempp.com/installation.html](https://bempp.com/installation.html).

## Documentation
Full documentation of Bempp can be found at [bempp.com/documentation](https://bempp.com/documentation/index.html)
and in [the Bempp Handbook](https://bempp.com/handbook). Automatically generated documentation of the Python API
can be found on [Read the Docs](https://bempp-cl.readthedocs.io/en/latest/).

## Testing
The functionality of the library can be tested by running:
```bash
python -m pytest test/unit
```
Larger validation tests that compare the output with the previous version of Bempp can be run with:
```bash
python -m pytest test/validation
```

## Getting help
Errors in the library should be added to the [GitHub issue tracker](https://github.com/bempp/bempp-cl/issues).

Questions about the library and its use can be asked on the [Bempp Discourse](https://bempp.discourse.group).

## Licence
Bempp-cl is licensed under an MIT licence. Full text of the licence can be found [here](LICENSE.md).


## Step-by-step user guide

1. **Create an isolated Python environment** using a Python version supported by this checkout, then install Bempp-cl from the repository root with <code>python -m pip install .</code>. Follow [INSTALLATION.md](INSTALLATION.md) if you need OpenCL drivers, optional packages, or a Numba-only configuration.
2. **Run a first example.** From the repository root, run <code>python examples/laplace/laplace_interior_dirichlet.py</code>. This solves a Laplace boundary-value problem on a sphere; the other [examples](examples/) cover mixed boundary conditions, Helmholtz, and Maxwell problems.
3. **Build the boundary-element model.** Load or generate a surface mesh, choose a function space and boundary data, then construct integral operators for the physical problem. Combine the operators into the boundary equation and solve it with a supported linear-algebra backend.
4. **Inspect the solution.** Evaluate the resulting grid function on the boundary or in the domain, compute the requested field or potential, and plot or export it. Check mesh resolution, boundary conditions, and solver residuals before interpreting the result.
5. **Choose the compute backend.** Bempp-cl uses JIT-compiled OpenCL kernels when a working OpenCL driver is available and can use Numba routines otherwise. Follow the installation guide to configure a backend and diagnose driver or compilation problems.
6. **Extend the formulation.** Reuse grid, space, operator, and solver building blocks for another supported kernel or boundary-value problem; keep mesh and units consistent.

### Functionality map

- Standard boundary integral kernels for Laplace, Helmholtz, modified Helmholtz, and Maxwell problems.
- Mesh/grid handling, function spaces, grid functions, boundary operators, blocked operator systems, boundary conditions, and iterative/direct solver interfaces.
- JIT execution through OpenCL or Numba, with examples for electrostatics, acoustics, and electromagnetics.
- Use [docs](docs/), [examples](examples/), the [Bempp Handbook](https://bempp.com/handbook), and the [Python API reference](https://bempp-cl.readthedocs.io/en/latest/) for the complete operator/function reference and advanced formulations.

