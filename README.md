# gnr-cw-decoder
This project is an attempt to understand how do develop a GNURadio CW Decoder.

As a keen Ham radio operator, and CW enthuiast over many years I have seen (and mostly laughed at) automated CW decoders. The 'language' is not overly complex - it is just that humans make it more difficult by their inaccurate keying techniques, this coupled with a variable symbol length (e is sent as . however a ? us ..--..).

But to start with I need to develop a basic CW flow.


#Generate the CW

You could of course use a radio and record some CW - however there is an excellent project at Git-Hub called [morsewav](https://github.com/cardre/morsewav.py.git). 

So I used that and then generated my test wav file.

The message I used was 

    test de a45wg a45wg
    
#Gnu-Radio

I am not going to inform you how to build/install Gnu-Radio as there are plenty of other sites out there. I am however going to assume you have little or no Knowledge of this product (as do I).

##Basic CW 



