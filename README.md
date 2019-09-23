# iRule-rewrite-links-and-redirects
Proxies communication of multiple internal websites that depend on redirects and internal links to jump between services.

Without using cookies this will replace internal links responses with the FQDN of the loadbalancer in front.

http://10.10.1.1/index.html >> https://website.example.com/index.html

This will also rewrite any redirect responses by encrypting the internal destination header and append it to the link, 
then it will decrypt the header and change the destination to the new IP

1. Location: http://10.10.2.2/newsite/index.html 
      >> Location: https://website.example.com/C.MTAuNDAuMS4xMjA=/newsite/index.html

2. https://website.example.com/C.MTAuNDAuMS4xMjA=/newsite/index.html  
      >> https://website.example.com/newsite/index.html & node 10.10.2.2
