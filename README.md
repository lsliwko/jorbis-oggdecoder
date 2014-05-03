jorbis-oggdecoder
=================

Extend jorbis library for OpenAL support


Compilation of several sources into one jar to simplify OGG Vorbis files play with OpenAL.
(version 1.1 compatible with Java 1.5)

_Example of use:_
{{{

// Create OGG Decoder
OggDecoder oggDecoder = new OggDecoder();

// Decode OGG into PCM
InputStream inputStream = new ByteArrayInputStream(bytes);

oggData = oggDecoder.getData(inputStream);
			
// Load PCM data into buffer
AL10.alBufferData(
    bufferId,
    oggData.channels>1?
        AL10.AL_FORMAT_STEREO16 : AL10.AL_FORMAT_MONO16,
    oggData.data,
    oggData.rate);
if (AL10.alGetError() != AL10.AL_NO_ERROR) {
    //Error check
}

}}}

_Special thanks to jcraft's people and Kevin Glass for this library._

----

=Issues in versions 1.0 and 1.1:=
Problems decoding lower bit-rates (like 8kHz) - change static ints 4096 everywhere in the code to 512 (all java files) or lower values (64, 128). Unfortunately, the jorbis libs have 4096 block size hardcoded and those classes are used in quite a lot applications. Therefore setting this value dynamically might have unexpected results.
_Thanks to Serkan Ucpinar for note about this!_