An encryption oracle is a type of attack that occur when a user-controllable input is encrypted and the resulting ciphertext is then made available to the user in some way.

This becomes dangerous when there are other user-controllable inputs in the application that expect data encrypted with the same algorithm. In this case, an attacker could potentially use the encryption oracle to generate valid, encrypted input and then pass it into other sensitive functions.

The danger also increases if there is a functionality on the site that provides a decryption function, which would enable to attacker to easily identify the expected data structure. The severity of an encryption oracle depends on what functionality also uses the same algorithm as the oracle.
## Examples from PortSwigger Web Academy
[![Authentication bypass via encryption oracle (Video solution, Audio)](https://img.youtube.com/vi/62spVp-GVPI/0.jpg)](https://www.youtube.com/watch?v=62spVp-GVPI)