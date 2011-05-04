Padding methods for password based encryption

I. Functions:
appendPadding(str, blocksize=AES_blocksize, mode='CMS'):
 Pad (append padding to) string for use with symmetric encryption algorithm
    Input: (string) str - String to be padded
           (int)    blocksize - block size of the encryption algorithm. Usually 8 or 16 bytes
           (string) mode - padding scheme one in (CMS, Bit, ZeroLen, Null, Space, Random)
    Return:(string) Padded string according to chosen padding mode

removePadding(str, blocksize=AES_blocksize, mode='CMS'):
  Remove padding from string 
  Input: (str) str - String to be padded
         (int) blocksize - block size of the algorithm. Usually 8 or 16 bytes
         (string) mode - padding scheme one in (CMS, Bit, ZeroLen, Null, Space, Random)
  Return:(string) Decrypted string without padding

II. Blocksizes:
DES (Triple DES), CAST5 and Blowfish have block size of 64 bits = 8 bytes
DES_blocksize = 8 
CAST5_blocksize = 8
Blowfish_blocksize = 8

AES has fixed block size of 128 bits = 16 bytes and this is the default blocksize
AES_blocksize = 16

III. Mode:
MODES ={
(0,'CMS')     : 'Pad with bytes all of the same value as the number of padding bytes. Default mode used in Cryptographic Message Syntax (CMS as defined in RFC 5652, PKCS#5, PKCS#7 and RFC 1423 PEM)',
(1,'Bit')     : 'BitPadding: Pad with 0x80 (10000000) followed by zero (null) bytes. Described in ANSI X.923 and ISO/IEC 9797-1',
(2,'ZeroLen') : 'Pad with zeroes except make the last byte equal to the number (length) of padding bytes',
(3,'Null')    : 'Pad with null bytes. Only for encrypting of text data.',
(4,'Space')   : 'Pad with spaces. Only for encrypting of text data.',
(5,'Random')  : 'ISO 10126 Padding (withdrawn in 2007): Pad with random bytes + last byte equal to the number of padding bytes'         
       }

CMS mode is the default one

IV. Examples:
Example 1: Add/Remove padding for message to be encrypted/decrypted with AES
> from Padding import appendPadding, removePadding
> msg = 'a'*20
> 
> padded_msg = appendPadding(msg) # 'Default blocksize is 16 bytes (128 bits) which is AES blocksize'
> padded_msg, len(padded_msg)
> msg = removePadding(padded_msg)
> msg, len(msg)

Example 2:  Add/Remove padding for message to be encrypted/decrypted with DES (Triple DES), CAST5 or Blowfish
> import Padding
> msg = 'b'*20
> blocksize = Padding.DES_blocksize
> "DES has fixed block size of %d bits = %d bytes" % (blocksize*8, blocksize)  
> padded_msg = Padding.appendPadding(msg, blocksize)
> padded_msg, len(padded_msg)
> msg = Padding.removePadding(padded_msg)
> msg, len(msg)