<!-- @TODO: Link XSS from Client-side vulnerabilities -->
With file upload vulnerabilities, an attacker may still be able to upload scripts for client-side attacks. For example, if an attacker can upload HTML or SVG files, they can potentially use `<script>` tags to create stored XSS payloads.

<!-- @TODO: Link CORs from Client-side vulnerabilities -->
If the uploaded file then appears on a page visited by users, their browser will execute the script when it tries to render the page. However, due to same-origin policy restrictions, these attacks will only work if the uploaded file is served from the same origin where the file is uploaded.