The first step to securing a pipeline is to secure the source code. In the event a threat actor (TA) can compromise the source code, they are in position to compromise the pipeline itself. We want to protect our source code from two main issues:

1. **Unauthorized Tampering** - Only authorized users should be able to make changes to the source code. This means that we want to control who has the ability to push new code to our repo.
2. **Unauthorized Disclosure** - Depending on the application, the source code might be considered sensitive information. In situations where this is the case, we must ensure that the source code is not intentionally or accidentally disclosed to the public.

**Confusion of Responsibilities**
Another common mistake made by large organizations is believe that the perimeter is a sufficient security boundary. This false belief can lead to misconfigurations, such as:

**Leaving the registration open for their self-hosted GitLab server**
Even if its hosted inside an intranet, if the access to GitLab allows

it allows any user in the intranet to register a profile. While some would not consider this a risk,