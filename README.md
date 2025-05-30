# cosmofoptscope

A Python package for analyzing First Order Phase Transitions (FOPT) in cosmological contexts. Built upon the CosmoTransitions package, this tool calculates nucleation temperatures for various theoretical models and computes essential phase transition parameters including phase transition strength ($\alpha$) and inverse duration of phase transition ($\beta$).

## Features

- Built on CosmoTransitions framework for reliable phase transition analysis
- Calculation of nucleation temperature for different theoretical models
- Computation of phase transition strength ($\alpha$)
- Evaluation of inverse duration of phase transition ($\beta$)
- Analysis of tunneling actions
- Multiple phase studies
- Support for parallel computation
- Customizable potential implementation

## Package Structure

```
.
├── cosmofoptscope
│   ├── find_fopt.py      # Core implementation for FOPT analysis
│   ├── __init__.py       # Package initialization
│   └── potential.py      # Potential wrapper and utilities
├── dist                  # Distribution builds
├── LICENSE              
└── pyproject.toml        # Project metadata and dependencies
```

## Installation

```bash
pip install cosmofoptscope
```

### Dependency Conflicts?

If you experience version conflicts with dependencies (numpy, scipy, ray, or cosmoTransitions), we recommend using uv for installation:

1. Install uv:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

2. Create and activate a virtual environment:
```bash
uv venv
source .venv/bin/activate  # On Unix/macOS
# or
.venv\Scripts\activate     # On Windows
```

3. Install cosmofoptscope:
```bash
uv pip install cosmofoptscope
```

## Quick Start

### Basic Usage

```python
from cosmofoptscope import FOPTFinder, PotentialWrapper

# Define your potential
class CustomPotential(PotentialWrapper):
    def Vtot(self, X, T):
        # Define your temperature-dependent potential
        pass

# Initialize FOPT finder
finder = FOPTFinder(
    potential=CustomPotential(),
    Tmax=1000,  # Maximum temperature
    g_star=100, # Effective degrees of freedom
    Mp=2.435e18 # Planck mass
)

# Calculate phase transition parameters
results = finder.report()
print(f"Nucleation Temperature: {results['Tnuc']}")
print(f"Critical Temperature: {results['Tcrit']}")
print(f"Phase Transition Strength (α): {results['alpha']}")
print(f"Inverse Duration (β): {results['beta']}")
```

### Parallel Computation

```python
# Enable parallel processing for faster computation
finder = FOPTFinder(
    potential=CustomPotential(),
    Tmax=1000,
    parallel=True
)
```

## API Reference

### FOPTFinder

The main class for phase transition analysis. Key methods include:

```python
class FOPTFinder:
    def __init__(self, potential, Tmax, g_star, Mp, parallel=False):
        """
        Initialize the FOPT finder.
        
        Args:
            potential: PotentialWrapper instance
            Tmax: Maximum temperature to consider
            g_star: Effective degrees of freedom
            Mp: Planck mass
            parallel: Enable parallel computation
        """
        pass

    def findTnuc(self):
        """Calculate nucleation temperature"""
        pass

    def findActions(self):
        """Compute tunneling actions"""
        pass

    def report(self):
        """Generate comprehensive report of transition parameters"""
        pass
```

### PotentialWrapper

Base class for defining potentials. Inherits from CosmoTransitions' generic_potential:

```python
class PotentialWrapper:
    def Vtot(self, X, T):
        """
        Define temperature-dependent potential
        
        Args:
            X: Field value
            T: Temperature
        """
        pass

    def alpha(self, temp, g_star):
        """
        Calculate phase transition strength
        
        Args:
            temp: Temperature
            g_star: Effective degrees of freedom
        """
        pass
```

## Examples

Find example implementations in the `examples` directory:

```python
# Example: Simple double-well potential
from cosmofoptscope import FOPTFinder, PotentialWrapper
import numpy as np

class DoubleWellPotential(PotentialWrapper):
    def Vtot(self, X, T):
        lambda_ = 0.1
        m2 = -1.0
        return 0.25 * lambda_ * X**4 + 0.5 * m2 * X**2 + 0.5 * T**2 * X**2

finder = FOPTFinder(potential=DoubleWellPotential(), Tmax=100)
results = finder.report()
```

## Dependencies

- numpy
- scipy
- ray (for parallel computation)
- cosmoTransitions (base framework for phase transition calculations)

## Contributing

We welcome contributions! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

Steps to contribute:
1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

[MIT License](LICENSE)

## Citation

If you use cosmofoptscope in your research, please cite:

```bibtex
@software{cosmofoptscope,
  title = {cosmofoptscope: A Python Package for Cosmological First Order Phase Transitions},
  year = {2024},
  url = {https://github.com/hiilynn/cosmoT-FOPTscope}
}
```


## Acknowledgments

- CosmoTransitions package for providing the fundamental framework

For more information and updates, visit our [GitHub repository](https://github.com/hiilynn/cosmoT-FOPTscope).
