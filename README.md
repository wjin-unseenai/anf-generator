# anf-generator
Generating coherence-constrained multisensor signals. Reference: https://israelcohen.com/wp-content/uploads/2018/05/JASA_Nov2008.pdf

## Example Code
```ruby
import numpy as np
import anf_generator as anf

# Define signals
duration = 10  # Duration in seconds
num_channels = 4  # Number of microphones

# Define target spatial coherence
params = anf.CoherenceMatrix.Parameters(
  mic_positions=np.array([[0.04 * i, 0, 0] for i in range(num_channels)]),
  sc_type="spherical",
  sample_frequency=16000,
  nfft=1024,
)

# Generate "num_channels" mutually independent input signals of length "duration"
input_signals = np.random.randn(num_channels, duration * params.sample_frequency)

# Generate output signals with the desired spatial coherence
output_signals, coherence_target, mixing_matrix = anf.generate_signals(
  input_signals, params, decomposition='evd', processing='balance+smooth')
```

Two more test scripts are provided: `tests/example.py` and `tests/example_babble.py`.

## References
<a id="1">[1]</a> E.A.P. Habets, I. Cohen and S. Gannot, *'Generating nonstationary multisensor signals under a spatial coherence constraint,'* The Journal of the Acoustical Society of America, Vol. 124, Issue 5, pp. 2911-2917, Nov. 2008. [Code](https://github.com/ehabets/ANF-Generator/releases/tag/v2008)

<a id="2">[2]</a> D. Mirabilii, S. J. Schlecht, E.A.P. Habets, *'Generating coherence-constrained multisensor signals using balanced mixing and spectrally smooth filters'*, The Journal of the Acoustical Society of America, Vol. 149, 1425, 2021.
