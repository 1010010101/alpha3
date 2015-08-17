# alpha3
Automatically exported from code.google.com/p/alpha3

[Usage]
  ALPHA3.py  [ encoder settings | I/O settings | flags ]

[Encoder setting]
  architecture              Which processor architecture to target (x86,
                            x64).
  character encoding        Which character encoding to use (ascii, cp437,
                            latin-1, utf-16).
  casing                    Which character casing to use (uppercase,
                            mixedcase, lowercase).
  base address              How to determine the base address in the decoder
                            code (each encoder has its own set of valid
                            values).

[I/O Setting]
  --input="file"            Path to a file that contains the shellcode to be
                            encoded (Optional, default is to read input from
                            stdin).
  --output="file"           Path to a file that will receive the encoded
                            shellcode (Optional, default is to write output
                            to stdout).

[Flags]
  --verbose                 Display verbose information while executing. Use
                            this flag twice to output progress during
                            encoding.
  --help                    Display this message and quit.
  --test                    Run all available tests for all encoders.
                            (Useful while developing/testing new encoders).
  --int3                    Trigger a breakpoint before executing the result
                            of a test. (Use in combination with --test).

[Notes]
  You can provide encoder settings in combination with the --help and --test
  switches to filter which encoders you get help information for and which
  get tested, respectively.

Valid base address examples for each encoder, ordered by encoder settings,
are:

[x64 ascii mixedcase]
  AscMix (r64)              RAX RCX RDX RBX RSP RBP RSI RDI

[x86 ascii lowercase]
  AscLow 0x30 (rm32)        ECX EDX EBX

[x86 ascii mixedcase]
  AscMix 0x30 (rm32)        EAX ECX EDX EBX ESP EBP ESI EDI [EAX] [ECX]
                            [EDX] [EBX] [ESP] [EBP] [ESI] [EDI] [ESP-4]
                            ECX+2 ESI+4 ESI+8
  AscMix 0x30 (i32)         (address)
  AscMix Countslide (rm32)  countslide:EAX+offset~uncertainty
                            countslide:EBX+offset~uncertainty
                            countslide:ECX+offset~uncertainty
                            countslide:EDX+offset~uncertainty
                            countslide:ESI+offset~uncertainty
                            countslide:EDI+offset~uncertainty
  AscMix Countslide (i32)   countslide:address~uncertainty
  AscMix SEH GetPC (XPsp3)  seh_getpc_xpsp3

[x86 ascii uppercase]
  AscUpp 0x30 (rm32)        EAX ECX EDX EBX ESP EBP ESI EDI [EAX] [ECX]
                            [EDX] [EBX] [ESP] [EBP] [ESI] [EDI]

[x86 latin-1 mixedcase]
  Latin1Mix CALL GetPC      call

[x86 utf-16 uppercase]
  UniUpper 0x10 (rm32)      EAX ECX EDX EBX ESP EBP ESI EDI [EAX] [ECX]
                            [EDX] [EBX] [ESP] [EBP] [ESI] [EDI]
