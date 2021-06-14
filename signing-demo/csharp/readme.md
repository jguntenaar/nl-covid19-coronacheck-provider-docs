﻿# CMS Signer tool

This is a small tool, it takes a file as input along with two certificates (your signing cert and a cert containing the full chain). 
It then signs the file and packs it in the JSON wrapper format defined by our APIs. Then, finally, it outputs that to std-out.

It can also validate the signature containined in the JSON wrapper against the given certificates if called with the `-v` flag.

It serves as an easily runnable example of how the signing works, implemented in C#. 

# Building

Install the .Net SDK for your platform (.net 5) then execute `publish.bat` or `publish.sh` (after making it executable!) as 
appropriate to build + publish the tool.

# Usage

Using the publish output (`publish/CmsSigner`)..

To produce a signed payload:

    CmsSigner -i file_to_sign -s path-to-x509-CMS-certificate -p password -c path-to-x509-CMS-chain

e.g.

    CmsSigner -i Example/test.txt -s Example/sign.pfx -p corona2020 -c Example/chain.p7b > file.json

The output can be piped to a file.

To check that a signature in the json wrapper you just made (the output from this tool in signing mode) is valid:

    CmsSigner -v -i file-containing-json-wrapper -s path-to-x509-CMS-certificate -p password -c path-to-x509-CMS-chain

e.g.

    CmsSigner -v -i file.json -s Example/sign.pfx -p corona2020 -c Example/chain.p7b

There is an example in the folder /Example (including test certificate + example certificate/chain) which generates the wrapper than
validates it. This is included in the output directory when you build/publish this project.



