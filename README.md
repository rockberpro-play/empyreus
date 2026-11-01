<p align="center">
  <img src="img/empyreus.png" alt="Empyreus" width="128">
</p>

<h1 align="center">Empyreus</h1>

<p align="center">A simple desktop tool to encode and decode subliminal audio.</p>

## About

Empyreus is a small GUI application built with Tkinter and [ttkbootstrap](https://github.com/israel-dryer/ttkbootstrap). It hides an audio track (such as speech) in the near-ultrasonic band by modulating it onto a 17.5 kHz carrier, following the logic of the Nyquist subliminal plugin. The same tool can demodulate the result back to audible audio.

## How it works

**Encode** (`encoder.py`)

1. Load the WAV file (sample rate must be at least 44100 Hz) and convert it to mono float.
2. Apply an 80 Hz high-pass filter.
3. Apply an iterative low-pass filter at `min(carrier / 2, sample_rate / 2 - carrier)`.
4. Multiply the signal by 2 and by a 17.5 kHz sine carrier.
5. Apply an iterative high-pass filter at the carrier frequency.
6. Normalize and save as a 16-bit WAV.

**Decode** (`decoder.py`)

1. Multiply the modulated signal by the same carrier.
2. Apply an iterative low-pass filter to recover the baseband signal.
3. Remove the DC offset and divide by 2.
4. Apply an 80 Hz high-pass filter.
5. Normalize and save as a 16-bit WAV.

## Requirements

- Python 3
- Dependencies listed in `requirements.txt`: `ttkbootstrap`, `numpy`, `scipy`, `pyinstaller`

## Getting started

```sh
pip install -r requirements.txt
python main.py
```

## Usage

1. Click **Input file** and select the source WAV file.
2. Click **Output file** and choose where to save the result.
3. Click **Encode** to generate subliminal audio, or **Decode** to recover audio from a subliminal track.

A dialog confirms when the file has been saved.

## Building a Windows executable

Run `bundle.cmd`. It uses PyInstaller to create a single-file, windowed executable in `dist/`.

## Project structure

| Path         | Description                      |
| ------------ | -------------------------------- |
| `main.py`    | GUI entry point                  |
| `encoder.py` | Subliminal audio encoding        |
| `decoder.py` | Subliminal audio decoding        |
| `img/`       | Application icon and attribution |
| `bundle.cmd` | PyInstaller build script         |

## Credits

The icon is [Radar](https://www.flaticon.com/free-icon/radar_196345) from Flaticon. The radar is a visual pun: Empyreus (from the Latin for "Empyrean") is a tool that leads toward the heavens, freeing the mind by untangling the subconscious.

## License

[MIT](LICENSE) © Rockberpro
