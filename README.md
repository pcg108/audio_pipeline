
# Audio pipeline

The audio pipeline is responsible for producing spatialized audio for XR experience.

# Components

## libspatialaudio

Submodule libspatialaudio provides the backend library for Ambisonics encoding, decoding, rotation, zoom, and binauralizer(HRTF included).

## audio pipeline code

### sound.cpp 

Describes a sound source in the ambisonics sound-field, including the input file for the sound source and its position in the sound-field.

### audio.cpp

Encapsulate preset processing steps of sound source reading, encoding, rotating, zooming, and decoding.

# Installation

Install libspatialaudio

    cmake CMakeLists.txt
    cmake -DCMAKE_INSTALL_PREFIX=/path-to-installation-directory
    make && make install

Add libspatialaudio in library path

    export CPATH=$INCLUDE_PATH:/path-to-installation-directory/include
    export LIBRARY_PATH=$LIBRARY_PATH:/path-to-installation-directory/lib
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/path-to-installation-directory/lib

Make audio pipeline files
    
    make

# Usage

    ./audio <number of 1024-sample-block to process> <optional: decode/encode>

Number of blocks to process is a must-have parameter. decode/encode specifies the different audio processing procedures to take on, which is specificially designed for profiling. And no output would be generated.

If encode or decode is not specified, the code will do both encode and decode on preset input sound sample files and generate a spatialized output audio at `output.wav`.

## Example:

    ./audio 500 

This will generate a ~10 seconds spatialized audio output from two sound samples under `./sample/`

    ./audio 2000 encode

This will encode 2000 sample blocks of audio input into ambisonics format.

## Notes

The input and output are hardcoded to be 48000 sample rate, 16-bit PCM wav file.

Also if you want to hear the output sound, limit the process sample blocks so that the output is not longer than input! Otherwise, garbage sound samples would be generated.

# Sound sample license

Sound samples under `./sample/` are obtained under Creative Commons 0 license.
