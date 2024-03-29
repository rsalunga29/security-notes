With file upload vulnerabilities, an attacker may still be able to upload scripts for client-side attacks. For example, if an attacker can upload HTML or SVG files, they can potentially use `<script>` tags to create stored [XSS](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-Site%20Scripting%2FIntroduction) payloads.

If the uploaded file then appears on a page visited by users, their browser will execute the script when it tries to render the page. However, due to [same-origin policy](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-Origin%20Resource%20Sharing%20(CORS)%2FSame-origin%20Policy%2FIntroduction) restrictions, these attacks will only work if the uploaded file is served from the same origin where the file is uploaded.