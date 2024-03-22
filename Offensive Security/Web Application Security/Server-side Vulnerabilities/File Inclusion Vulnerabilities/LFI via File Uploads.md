For LFI to work in file uploads, the file upload form do not need to be vulnerable, but merely allow us to upload files. If the vulnerable function has code `Execute` [capabilities](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FFile%20Inclusion%20Vulnerabilities%2FRead%20vs%20Execute), then the code within the file we upload will get executed if we include it, regardless of the file extension or file type.

For example, we can upload an image file (e.g. `image.jpg`), and store a PHP web shell code within it 'instead of image data', and if we include it through the LFI vulnerability, the PHP code will get executed and we will have remote code execution.
## Crafting Malicious Image
