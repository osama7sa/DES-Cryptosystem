# DES-Cryptosystem
Implementation of DES encryption in python.


he scenario of the program is to encrypt passwords. The
program will read the password from file where the user will
write the password. As we know, the password cannot contain
any spaces so the program will remove any whitespace. Then
the password will go through the program as plaintext to apply
each step of DES algorithm. 


Implementation:
For example, I will encrypt this password:
osamaabdullah1823

Using this key: BCAECDAEBBABCBAD
First step the program will read the password from the file (password.txt)

Then it will remove the whitespace. Now because the password
is text so we have to convert it to hex.

[6f73616d61616264756c6c616831383233]

If the password is more than 16 hex like in this situation the
program will split the plaintext into parts every part 16 hex to
encrypt every part separately.
[6f73616d61616264,756c6c6168313832,33]
Now we have a problem with the last part have only 2 hex. In
this case, the program will do padding to fill last part with (0)
until it reaches 16 hex (64-bit).
[6f73616d61616264,756c6c6168313832, 0000000000000033]

Key generation:
Key input 56-bit  output 48-bit

Now we have plaintext (64-bit) and (48-bit) key
in binary. The plaintext will pass through an
initial permutation (IP) that rearranges the
bits. The plaintext will split into two parts
each part 32-bit Then right part will go
through the round to implement the DES round
steps.
The last step the plaintext pass through final
permutation.
Result after encryption and combine parts together:
[15931A9618B21B3232B63C1ABE32BE9BA02A2088AA28AA19]

Permutation function used to:
key permutation with (PC1)
key=permutation(key, PC1, 56)

Key permutation with (PC2)
key=permutation(key, PC2, 48)

Plaintext permutation (initial permutation)

plain_text[i] = permutation(plain_text[i], initial_permutation, 64)

Right plaintext Expansion (E-table)
right = permutation(right, expansion, 48)

Right plaintext substitution (S-Box)
right = substitution(right)

Right Plaintext permutation after substitution
step
right = permutation(right, p_box, 32)

Final permutation after combine left and right
final_plaintext = permutation(final_plaintext, final_Permutaion, 64)

Xor function used to:
-XORing between 48-bit right plaintext after
expansion and the generated key for the round
right = xor(right, key)

-XOR operation between left plaintext and right
after pass through the round
round1 = xor(right, left)



