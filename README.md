<h1> Wordpress Pentesting </h1>

<h3> Time: approx 14 hours </h3>

<h3> 1. Stored XSS </h3>
<p>Discovered by Jouko Pynnönen of Klikki Oy  <a href=url>https://klikki.fi/adv/wordpress2.html</a> This site was used as a resource.
      I injected this code into the a post.
  <a title='x onmouseover=alert(unescape(/hello%20world/.source)) style=position:absolute;left:0;top:0;width:5000px;height:5000px [64 kilobytes of Letters]’></a>
  You need 64 kilobytes of letters so I made that with this python command.
  In vim you can open up payload.txt and use ":%+" to copy the entire file and then paste it where the letters go in the payload.

</p>
