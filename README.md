# gnr-cw-decoder
This project is an attempt to understand how do develop a GNURadio CW Decoder.

As a keen Ham radio operator, and CW enthuiast over many years I have seen (and mostly laughed at) automated CW decoders. The 'language' is not overly complex - it is just that humans make it more difficult by their inaccurate keying techniques, this coupled with a variable symbol length ('e' is sent as '.' however a '?' is ..--..).

But to start with I need to develop a basic CW flow.


#Generate the CW

You could of course use a radio and record some CW - however there is an excellent project at Git-Hub called [morsewav](https://github.com/cardre/morsewav.py.git). 

So I used that and then generated my test wav file.

The message I used was 

    test de a45wg a45wg
    
#Gnu-Radio

I am not going to inform you how to build/install Gnu-Radio as there are plenty of other sites out there. I am however going to assume you have little or no Knowledge of this product (as do I).

##Basic CW



##Data Rate

```python
def cwlen(ch):
    if ch == '.':
        return 2
    elif ch == '-':
        return 4
    elif ch == ' ':
        return 6  # I am assuming a char came before which had a dot gap at its end.
    else:
        print(str.fomat('Unknown {}', ch))


CODE = {'A': '.-', 'B': '-...', 'C': '-.-.',
        'D': '-..', 'E': '.', 'F': '..-.',
        'G': '--.', 'H': '....', 'I': '..',
        'J': '.---', 'K': '-.-', 'L': '.-..',
        'M': '--', 'N': '-.', 'O': '---',
        'P': '.--.', 'Q': '--.-', 'R': '.-.',
        'S': '...', 'T': '-', 'U': '..-',
        'V': '...-', 'W': '.--', 'X': '-..-',
        'Y': '-.--', 'Z': '--..',
        '0': '-----', '1': '.----', '2': '..---',
        '3': '...--', '4': '....-', '5': '.....',
        '6': '-....', '7': '--...', '8': '---..',
        '9': '----.',
        ' ': ' '
        }

WPM = 25
# word="PARIS "*WPM
data_to_send = "TEST DE A45WG A45WG"
# All Timing are in DOT lengths
dot_len = 1
dash_len = 3
char_gap = 1
word_gap = 7  # BUT ONLY add 6 as we have already added 1 dot on the end of the character
to_send = []
total = 0

for c in data_to_send:
    try:
        send_len = [cwlen(a) for a in CODE[c]]
        #
        #That was all the letters  - now add 6 'dots'
        #The space between words should be 7 but we have added 1 already to the last letter.
        #
        print(str.format('{} -> {} -> {}', c, CODE[c], str(send_len)))
        for b in range (0, len(send_len)):
            send_len.insert(b*2+1, 1)
        to_send = to_send + send_len
    except Exception as err:
        print("Problem " + str(err))
        pass


print("20 WPM")
print(str.format("data to Send is <{}>", to_send))
#
# Now calc the total bits
#
total=0
for a in to_send:
    try:
        total = total + a
    except:
        pass
#
print(str.format("Paris sent at {} WPM is {} Bits", WPM, total))
```

