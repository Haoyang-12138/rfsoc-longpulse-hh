# rfsoc-longpulse-hh
Long Arbitrary Waveforms for QICK on RFSoC4x2：DAC A 6.6667us arb+ DAC B 80us arb+ 1 ADC(tproc v1)
The zip file include precompiled firmware (a bit file and hwh), a matching QICK Python library, and a Jupyter example.

## Quick start
1. Connect to the board's Jupyter interface over Ethernet.
2. Create a new folder on the board and upload all four files.
3. Open the example notebook with a fresh Python kernel.
4. Run the import/loading cell, then the waveform cell.
5. To stop output, run: stop_output()

Python runs on the RFSoC board. Use the supplied library rather than the system-installed QICK package. 

#Technical details:
## Hardware configuration
| Board: RFSoC4x2, XCZU48DR |
| Processor: tProc v1 |
| DAC B / CH0: 80 µs arbitrary-waveform memory |
| DAC A / CH1: 6.666667 µs arbitrary-waveform memory |
| ADC: One readout channel |
| DAC sample rate: 9.8304 GS/s |

- `qick_4x2_arb80_dac2_adc1.bit`: FPGA bitstream.
- `qick_4x2_arb80_dac2_adc1.hwh`: matching hardware description.
- `qick_lib_dac2adc1.zip`: matching QICK Python library.
- Example `.ipynb`: board initialization and waveform control.


## Modified Python library

The library patch changes `qick/drivers/generator.py` to read the custom `ENV_WORDS` parameter and report the correct waveform-memory capacity for DAC B. DAC A retains the original capacity calculation. The patch does not change the ADC driver or tProc instruction set.

## Status

The firmware was built with Vivado 2023.1 and passed the recorded static timing checks, with reported WNS of 0.000 ns. Full board-level validation, including ADC acquisition and analog phase repeatability, is pending. The chirp example has not yet been verified on hardware.

This release provides precompiled firmware and usage examples. FPGA build sources are not included.

## Upstream and attribution

Based on [QICK](https://github.com/openquantumhardware/qick), commit `bea61c157062c98d47f6dbb9a936a720e21fb49f`.

This is an independent extension of QICK. Upstream QICK code is distributed under its MIT license; retain the original copyright and license notices with redistributed code. Third-party components remain subject to their respective terms.
