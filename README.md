OP-1 Tools
===

At present, this is just notes about how to create a sample file that's suitable for dragging onto the OP-1's internal USB drive.

Note that I used Ubuntu for this research.

Creating a working sample
===

1. `sudo apt-get install espeak libav-tools`
1. `espeak -ven-us+f4 -w congrats.wav "Congratulations. Your OP-1 sample work
s"`
1. `avconv -i congrats.wav congrats.aif`
1. Plug in OP-1 to computer, shift-COM, drag `congrats.aif` to `synth/user`, eject drive, see working sample.

Converting an existing WAV
===

1. Download wav from [http://www.orangefreesounds.com/amen-break/] and rename to lowercase.
1. Confirm that the sample is 6 seconds or less in length.
1. `avconv -i amen-break.wav -ac 1 amen-break.aif`
1. Transfer to OP-1. Confirm it works.

Notes
===

There is a conversion process on the OP-1 after transfer that adds some metadata to the aif file. Here is what I saw after transferring the amen-break.aif file back to my computer:

    {
       "adsr":[
          64,
          10746,
          32767,
          10000,
          4000,
          64,
          4000,
          4000
       ],
       "base_freq":440.0,
       "fx_active":false,
       "fx_params":[
          8000,
          8000,
          8000,
          8000,
          8000,
          8000,
          8000,
          8000
       ],
       "fx_type":"delay",
       "knobs":[
          0,
          0,
          32767,
          32767,
          12000,
          0,
          0,
          8192
       ],
       "lfo_active":false,
       "lfo_params":[
          16000,
          0,
          0,
          16000,
          0,
          0,
          0,
          0
       ],
       "lfo_type":"tremolo",
       "name":"amen-break",
       "octave":0,
       "synth_version":2,
       "type":"sampler"
    }

For the `congrats.aif` file, the two 32767 values in the `knobs` list were 9335. I suspect that I fiddled with the knobs in between imports. I don't know what the knobs mean yet.

It is surprising that `amen-break.aif` does appear to be based at 440Hz (the higher A key on the keyboard), just as the JSON metadata suggests, but `congrats.aif` is based at 220Hz (the lower A on the keyboard). I can't figure out why this is the case.
