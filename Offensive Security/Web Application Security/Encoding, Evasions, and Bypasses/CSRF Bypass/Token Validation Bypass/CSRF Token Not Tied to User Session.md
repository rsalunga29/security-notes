Some applications do not validate that the token belongs to the same session as the user who's making the request. Instead, the application either only checks if the token is algorithmically correct or the application maintains a global pool of tokens that it had issued in the past and accepts any tokens that appears in this pool.

In this situation, the attacker can just get a valid token from their own account and feed that token to the victim user in their attack.