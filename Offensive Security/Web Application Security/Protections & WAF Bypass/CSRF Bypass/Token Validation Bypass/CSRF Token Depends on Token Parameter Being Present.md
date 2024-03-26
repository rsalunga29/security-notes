Some applications only validates the token parameter if it is present, but fails to validate if the token value is omitted or not, resulting in token validation being skipped.

In this situation, an attacker can just remove the entire parameter containing the token (not just its value) to bypass the validation.