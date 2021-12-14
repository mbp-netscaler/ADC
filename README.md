# ADC

UPDATE: Citrix have released a blog post with their own responder policies, which also includes body search, read their blog post here
https://www.citrix.com/blogs/2021/12/13/guidance-for-reducing-apache-log4j-security-vulnerability-risk-with-citrix-waf/
Citrix have also updated their signatures, so make sure you're on version 73, as they are better than what was first released.

I will most likely also update the responders here, because there seems to be an issue with the packet engine and the current version, and Gunther (https://twitter.com/gudepoortere?lang=en) made a new regex, that seems to work better with the packet engine, it hasn't been tested as much, so we'er unaware about false positives.

Update 2: I've added the policies from Citrix and modified the original with the new regex, so everyone can choose.

Update 3: Redone the v2 policies, as there was a false positive with MAPI - please update

With the whole Log4j issue, a lot of people have asked how they maybe do some kind of protection with their Citrix ADCs.
A group of us Citrix PTEC guys have been chatting over the weekend and Eric (https://www.linkedin.com/in/eric-julien-04b160/) made a regex that seems to work better than the Citrix AppFW signature as of now.

So to post some awereness about, i've put the responder and logging policies here, since all version of ADC will have those available.

What follows is not an absolute workaround, but it may help save time for your customers by blocking the scanning attacks using the URL or the headers as vectors.
I had to many false positive using the regex against POST bodies when binary/pfg files are uploded (i.e. breaks MAPI for instance)

the regexr.com tester of the regex

![REGEX](https://github.com/mbp-netscaler/ADC/blob/main/regex.jpg?raw=true)


The new regex

![REGEXv2](https://github.com/mbp-netscaler/ADC/blob/main/Gunter-regex.jpg?raw=true)

Note that each ? character in the regex  is escaped with \ so you can copy/paste through putty to the CLI

REMINDER : IT IS NOT AN ABSOLUTE PROTECTION BUT IT DOES COVER MORE CASES THAN THE APPFW SIGNATURE RELEASED YESTERDAY AND WORKS IN ANY ADC AS IT IS BASED ON RESPONDER
USE IT, MODIFY IT, BUT DON'T BLAME ME FOR ANYTHING ;-)


This is an issue that is best served by patching or disabling.

Also a huge thanks to Jan Tytgat (https://twitter.com/jantytgat) and Anton Van Pelt (https://twitter.com/AntonvanPelt), which all have contributed in our group.

