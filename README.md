# NGINX Secure Server Setup
#### Note
I shall revise this work, along with my PKIX project revision.
## Description
Hello and welcome.\
This is an NGINX setup that complies with Mozilla's server side security recommendation.\
## How Did I Set It Up
I used my pkix_setup.sh script to set up a local root CA (you can find it in my profile.)\
I used it to sign (1) an ECDH key; and (2) RSA key. This complies with Mozilla's modern and intermediate set of ciphersuits.\
The private keys are encrypted using AES and a 256-bit key. I set NGINX to use the passphrases. Check nginx.conf file.\
As for NGINX, I complied with Mozilla's security settings. Mozilla has a security generator that easens this task.\
I edited `/etc/hosts/` file so that my website can be easily accessible through my web browser and internet tools.\
As for the website's content, I got it from Free Code Camp's course on Nginx. This is not a sponsore, and I don't think that the course is paid. The course is awesome, I enjoyed it. You can find it here: https://www.freecodecamp.org/news/the-nginx-handbook/#heading-introduction-to-nginxs-configuration-files.
## How to install this on your machine
Running the `tree` command, you'll find many files. Let's see each one.\
    1. `nginx.conf` is the nginx configuration file, this file should be kept in `/etc/nginx/`.\
    2. `pki/` is a directory. Inside it is `pkix` another directory, and `pkix_setup.sh` my script. The former is generated using my script.\
    3. `sites-available/` this directory contains the configuration files for any sites. It contains the main config file that is set up by default + a server to serve the CRL.\
    4. `sites-enabled/` a directory that cotnains nothing but symlinks to the files in `sites-available`. This is important. Nginx knows which sites are enabled through this directory.\
    5. `srv/` a directory that contains the website's content. I got this from the Free Code Camp course. It should be stored in the root directory, i.e., `/etc/srv/...`
Place everything in the right place and you should be good to go. So you only need two things, (1) OpenSSL; and (2) NGINX.
## How to create a similar thing
Disclaimer, this is but an experiment. My private keys are well exposed, but since everything is but an experiment, I don't mind.\
Firstly: run my pkix_setup.sh script to set up a local root CA.\
Secondly: use OpenSSL to create Elliptic Curve parameters for Deffie Helmann, and RSA key.\
Thirdly: sign them using your local CA.\
Fourthly: head to https://wiki.mozilla.org/Security/Server_Side_TLS and comply with the recommendation. Mozilla is well respected.\
Fifthly: create a separate folder for the CRL and create a subdomain to access it. Here comes the need for `sites-enabled/` folder.\
Sixthy: edit on the `/etc/hosts` file such as your ip address refers to the DN of your site.\
Severnthly: open your browser, type `https://[DN]`, accept the risk. The rist is because you have self signed your CA's certificate.\
I think this is all..
