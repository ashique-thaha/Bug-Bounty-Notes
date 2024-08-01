
#### Whois, reverse whois, ASN etc.

 - [ ] Go for `NSLOOKUP`  and get an ip of target ex:(`nslookup facebook.com`)

 - [ ] Then do `whois facebook.com` This is called reverse ip search for to find domains hosted on the same server.

 - [ ] Also check for for a field called `NetRange`  from above ip search to get a dedicated ip range for the target.

 - [ ] `whois -h whois.cymru.com {ip}` This will provide us with ASN number and name, that will help us to identify if the same owner own the ip range.

 - [ ] Use `netcraft.com` for some additional information 

#### Certificate Parsing

- [ ] Go to `crt.sh ` and type domain name to find additional hostname that uses the same `SSL` certificates. Just add the URL parameter `output=json` to the request URL: `https://crt.sh/?q={domain name}&output=json.`

#### Subdomain Enumeration

- [ ] use tools like` Sublist3r, SubBrute, Amass, Gobuster` and sort it under a mind map as checked or not checked

- [ ] use `ceWL` for custom wordlist generation, use it for sub-domain enum.
#### Service Enumeration

- [ ] Use `Nmap` to enumerate services running on the machine 

- [ ] `Nmap` will be an active scan we can use `shodan` to enumerate services `passive` on the host giving its `ip address`

- [ ] `Censys` and `Project Sonar` are similar tools that will help.

- [ ] With these databases, also find the target’s `IP addresses` , ` certificates`and `software versions`
 
- [ ] use nmap's `http-methods` script for finding possible http methods, also don't forget to add http-methods.url-path as script argument. example: #example1

- [ ] if  the web app is using `word-press` then, to enumerate themes and plugins used use nmap's `http-wordpress-enum` script #example2

#### Directory Brute-Forcing

- [ ] use `Dirsearch ` or `Gobuster` for directory brute-forcing

- [ ] use` eyewitness` or `Snapper` to automatically verify that a page is hosted on each location, by `screenshotting`.

- [ ] use nmap's `http-enum` script to look for common directories.

- [ ] Use `wfuzz` to enumerate directories #example4 

#### Spidering the Site

- [ ] use `Zap's spider` or `burp's crawler` to spider the site.

- [ ] use `hakrawler`  to find previously used or archived domains , subdomains, endpoints etc. #example8

#### Third-Party Hosting

##### S3 buckets
- [ ] use google dorking  to find s3 buckets: ` site:s3.amazonaws.com COMPANY_NAME , site:amazonaws.com COMPANY_NAME`

- [ ] To find S3 buckets , search a company’s public `GitHub` repositories for `S3 URLs`

- [ ] Use `GrayhatWarfare`  to find publicly exposed S3 buckets.

- [ ] To brute-force buckets by using keywords, use  `Lazys3`

- [ ]  use `Bucket Stream` to parse certificates belonging to an organisation, and find S3 buckets based on permutations of the domain names found on the certificates.

- [ ] configure `awscli` first and the go for accessing aws from command line

- [ ] To access `aws` from command line use the command : `aws s3 ls s3://BUCKET_NAME/`

- [ ] If it works, try to read the contents of any interesting files by copying files to local machine: `aws s3 cp s3://BUCKET_NAME/FILE_NAME/path/to/local/directory`

- [ ] look for `API keys` or `personal information` from these buckets.

- [ ] Try to mess with files on the bucket, like if its able to delete or upload files 

- [ ] For this upload a file from local machine and try to delete it, so it won't corrupt the application.

	This command will copy your local file named `TEST_FILE` into the target’s S3 bucket:`aws s3 cp TEST_FILE s3://BUCKET_NAME/`  
	
	This command will remove the `TEST_FILE `that you just uploaded:`aws s3 rm s3://BUCKET_NAME/TEST_FILE`

#### GitHub Recon

- [ ] Search an organisation’s `GitHub repositories` for sensitive data that has been accidentally committed, or information that could lead to the discovery of a vulnerability

- [ ] Start by finding the `GitHub usernames` relevant to  target. To locate these, search the `organisation’s name` , `product names` via GitHub’s search bar, or by checking the `GitHub accounts of known employees`.

- [ ] After finding `usernames` to audit, visit their pages.` Find repositories` related to the `projects being tested ` and record them, along with the `usernames of the organisation’s top contributors`.

- [ ] Dive into the code, go thorough `issues and commit `sections. This will point to bugged and problematic codes here. check the `Blame and History` sections too.

- [ ] Look for hardcoded secrets such as `API keys, encryption keys, and database passwords`. Search the organisation’s repositories for terms like `key, secret, and password `to locate hardcoded user credentials that can use to access internal systems.

- [ ] use `KeyHacks` to check if the credentials are valid.

- [ ] See if any of the source code deals with important functions such as` authentication, password reset, state-changing actions, or private info reads`. 

- [ ] Pay attention to code that deals with `user input`, such as `HTTP request parameters, HTTP headers, HTTP request paths, database entries, file reads, and file uploads`. 

- [ ] Look for any `configuration files`, as they allow you to gather more information about the  infrastructure. Also, search for `old endpoints and S3 bucket URLs ` to  attack. 

- [ ] Tools like `Gitrob `and `TruffleHog` can automate the GitHub recon process. `Gitrob `locates potentially sensitive files pushed to public repositories on GitHub. 

- [ ] `TruffleHog `specialises in finding secrets in repositories by conducting regex searches and scanning for high-entropy strings

- [ ] Go to the targets `github` page and search for `filename:users` this will return files with usernames and maybe passwords

- [ ] 

#### OSINT Techniques

- [ ] check the organisations job posts for engineering positions (In  the qualification section we can see the tech stack required for the job and thus the company)

- [ ] Search for employees’ profiles on `LinkedIn`, and read employees’ personal blogs or their engineering questions on forums like `Stack Overflow` and `Quora`.

- [ ] check for employee `social media` profile

- [ ] check `google calendar` to know if any meeting or works are made public `accidentialy`.

- [ ] check the company’s `SlideShare` or `Pastebin` accounts

- [ ] Use  `Wayback Machine`, to find old endpoints, directory listings, forgotten subdomains, URLs, and files that are outdated but still in use.

- [ ] `Tomnomnom’s` tool` Waybackurls` to automate the process.

#### Tech Stack Fingerprinting

- [ ] Find software versions and tech stack running on the system for to find `CVE` or exposed `vulns`.

- [ ] run `nmap` version scan .

- [ ] check `http headers` like` X-Powered-By` to find underlying tech.

- [ ] check source code for clue of tech stack.

- [ ] check using `wappalyzer`

- [ ] use `retire.js` to find expired javascript.

- [ ] Use a tool on command line called `whatweb`. This will help in mainly tech stack finger printing and more.

- [ ] Find if any `login endpoint` related to `tech stack` available. if so look for `default credentials`.

#### File Discovery

- [ ] Use `wfuzz` to discover files on target by brute forcing #example3


#### Parameter Discovery

- [ ] use `wfuzz` to find hidden parameters. #example5

- [ ] use `wfuzz` to discover parameter values. #example6 

- [ ] fuzz the post data of the parameter using `wfuzz` #example7 


#### MISC
- [ ] Use `Spiderfoot` to automate entire recon phase.
