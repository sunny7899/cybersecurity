____________________________________________________________________

 

Removing Banners from your site By Ankit Fadia ankit@bol.net.in

____________________________________________________________________

 

Warning: Experienced Programmers might find this manual lame and I do not guarantee that these tricks will always work.

Today, there are a number of websites, which offer you free webspace and a reasonably good URL, for free. This service has become very popular as it is the easiest and fastest way of putting up your site on the net, getting an identity for yourself and becoming a part of the huge web.

 

However, like most good things, this too has a catch. These services require each page that you host on their server to have a banner or advertisement embedded in it. This not only affects the downloading time of the visitors (who visit your site), but also affects, the way you position various elements on a particular page. For Example, if the banner which is automatically embedded at the top of each page has too many colors, then you might have to change the color that you use for other elements of your page, so as to make them (the elements like Navigation Bar) more visible.

 

What is more, if you are using frames on your site, then each frame will have an individual banner embedded in it. This results in the positioning of various elements going haywire and makes your page look extremely pathetic. Talk about getting framed!!!! (This is one of the reasons as to why you should avoid using frames on your site)

 

Anyway, in this HT manual, we will learn just how to get rid of these irritating banners and to make your free webpage really kewl.

 

**********************
HACKING TRUTH: The banners which are embedded are just about the only source of income for these websites, so if you are caught carrying out any of the below 'No Banner' tricks, then you would possible lose your account. So BEWARE!!!
*********************

 

Anyway, the tricks that you can execute to prevent embedded banners from displaying vary from service to service. It basically depends on as to which website you have your account on. 

GEOCITIES

Place the below code after the end HTML tag:
<noscript>

Angelfire/FreeServers/50Megs/FortuneCity/Netscape

Place the below code anywhere on the page:

<script language="JavaScript">
function open() {} 
</script> 

 

The above snippet will give an error and normally no other JavaScipt code would be executed, so no banner would be displayed. However, it doesn't work in all cases, so there is yet another Hack for Angelfire: Sorround the BODY tag with the below code: 

 

<noscript></noscript>

TRIPOD

Same as ths second hack for Angelfire

XOOM

To prevent banners from displaying on your webpage hosted by XOOM, replace the standard URL with the below URL:

http://members.xoom.com/_XMCM/username/ 

 

Removing Pop Up Banners

Well, some of the above tricks also seem to stop pop up banners from being displayed. However, another option that could be propagated would be to ask all visitors to install a Software called AddsOFF which stops new windows (pop up ads) from being displayed. But again this is not a feasible option. Infact, some personal firewalls also filter out code which open pop up Banners. 


Getting a FREE (Banner Free) .COM registration

1. The NameZero Hack

 

Most of you must have heard of NameZero, which gives you a free .Com (or .Net or .ORG) registration and in return puts up a huge banner at the bottom of each page. Well, putting the following piece of code after the TITLE tag would do the trick for you: (Sometimes the following hack is said to not work, if that is the case then try the NameDemo hack instead. Either of the two will definitely work.)

<SCRIPT LANGUAGE="Javascript">
<!--
if (parent.frames.length) 
parent.location.href= self.location; 
// -->
</script>

 

2. The NameDemo Hack

 

Simply add the following to the first page of the home page of your site, after the <BODY> opening tag:

 

<script language="Javascript">

<!-- 

if (top.location != self.location) {

top.location = self.location.href

}

 

//--> 

</script>

Again, I would like to say that if any of these tricks do not work, then kindly do not flame me. This manual was aimed at simply giving you a general idea as to how to go about removing banners. It is basically for getting you started. 

 

Ankit Fadia

ankit@bol.net.in

http://www.ankitfadia.com

 

To receive tutorials written by Ankit Fadia on Everything you ever dreamt of in your Inbox, join his mailing list by sending a blank email to: programmingforhackers-subscribe@egroups.com
