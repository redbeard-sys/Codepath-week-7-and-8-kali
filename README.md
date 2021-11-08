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
      
   ![Image Walkthrough](https://github.com/redbeard-sys/Codepath-week-7-and-8-kali/blob/main/password.gif)
     
      
      
  <h2> 3. Another Stored XSS </h3>
      <h4> versions before 4.2.3 are affected</h4>
     Also discovered by Jouko Pynnönen of Klikki Oy  <a href=url>https://klikki.fi/adv/wordpress3.html</a> 
      The following code was inculcated into a post:
  ![Image]()
       Wordpress processes this code into the following form
      
  ![Image Walkhtrough](https://github.com/redbeard-sys/Codepath-week-7-and-8-kali/blob/main/storedXSS.gif)


