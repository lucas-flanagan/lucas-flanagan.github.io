---
layout: default
---

## Creating an Account

If you're new to HTB and have recently attempted to create an account, you've likely come to the realization that the website will test your knowledge and willingness to learn at every step. As such, you're challenged to hack your way into making an account.

Let the fun begin.

<img src="/images/createacc.png">

Looks like we're searching for some sort of code that will allow us to sign up.
A good first step would be to check out the source code.

<img src="/images/firsthint.png">

I right clicked and selected the inspector tool.
There's a subtle hint here in the 'console section' that states the following:
<p class="message">This page loads an interesting javascript file. See if you can find it :)</p>

Alright, so lets check out the website's javascript files. 
<img src="/images/jsfile.png">

Here's a link to one of the JS source files from the source HTML. Lets open the link in a new tab to examine the code.

<img src="/images/js.png">

I had to google 'obfuscated'. If you dont already know, it means unintelligible. 

Lets copy paste the code into a javascript beautifier so its easier to read.

<p class="message">
//This javascript code looks strange...is it obfuscated???

function makeInviteCode() {
    $.ajax({
        type: "POST",
        dataType: "json",
        url: '/api/invite/how/to/generate',
        success: function(a) {
            console.log(a)
        },
        error: function(a) {
            console.log(a)
        }
    })
}
</p>
Beautiful indeed.

As you can see, there's a javascript function called makeInviteCode. Im going to take a wild guess and say that we need to call that function somehow so it can make an invite code for us.

JS functions can be called in the console area where we found that first clue. Lets do that and see what happens.

<img src="/images/makeinvitecode.png">

Nice. Looks like we have some sort of encrypted message. They gave us the encryption type which makes it easier.

<p class ="message">
  Va beqre gb trarengr gur vaivgr pbqr, znxr n CBFG erdhrfg gb /ncv/vaivgr/trarengr
  Encryption type: ROT13
</p>

I looked up "ROT13 decoder" and copy pasted the message.

Here's the result:
<p class ="message">
  In order to generate the invite code, make a POST request to /api/invite/generate
</p>

Great, another hint. They're really making us work for this one.

If you dont know what a POST request is, check out <a href="https://www.w3schools.com/tags/ref_httpmethods.asp">this</a> article.

We can make a post request using <a href="https://www.geeksforgeeks.org/curl-command-in-linux-with-examples/">curl</a>.

This is the command I used to make the post request.
<p class ="message">
  curl -XPOST https://www.hackthebox.eu/api/invite/generate
</p>

Looks like I got a data output with a "code". Initially I tried to use this as the sign up key, but it didnt work. Looking back, I noticed that the format is "encoded". 

I put the data into an online "cipher identifier" to try to figure out how it has been encoded

<img src="/images/base64.png">


Base64 it is. Lets punch it into a base64 decoder.

After decoding, the value worked on the HTB signup page! Now I can make an account.

Good luck and thanks for reading!





