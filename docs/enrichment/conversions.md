# The many ways to calculate conversions

Conversions tracking is all about reporting on performance of your communications and marketing.  If you're not tracking conversions, you're basically spraying and praying.  Below we'll cover some common conversion mechanisms, and their pros and cons.

For the purposes of this document, we're going to talk about monetary transactions (purchases, donations, etc), but the same concepts apply to other conversion types (lead generation, signup forms, petitions, etc).

## Native conversion tracking

Some integrated platforms natively track the conversion performance of a message.  For example, an integrated email and transaction processor can track an individual from the email they click on all the way through to a completed transaction.  Usually this is done with cookies, sometimes with URL parameters, sometimes with javascript, etc, etc.  But fundamentally the platform is in charge of the process from end to end.

This is very convenient if you're using the same platform for everything, but it doesn't map well to social media tracking, or to multiple different messaging and transaction platforms.

## Tag & Pixel conversion tracking
[Google (Tag manager)](https://support.google.com/google-ads/answer/6095821) and [Facebook (Pixel tracking)](https://developers.facebook.com/docs/facebook-pixel/implementation/conversion-tracking/) are a few of many popular tools that exist to track conversions in a multi-channel environment.  They work by placing a chunk of code, or a pixel, on the page AFTER someone makes a transaction.  The tool will then store information about that conversion, which you can gather reporting on.

If the messaging is going out of the same platform you're tracking on, for example if you're posting a Facebook Ad and using the Facebook pixel, you can see direct conversion performance right next to the ad performance -- making it easy to calculate Return-On-Investment (ROI).

Tag & Pixel is a very common and very effective means of calculating performance.  However, it suffers from a few problems:

	1) Privacy -- More and more people are becoming sensitive to ubiquitous tracking on the web, and are disabling third party trackers, or explicitly disabling Google and Facebook tracking.  While historically small, this has an increasing effect on the accuracy of T&P tracking.

	2) Only on the web -- Many groups organize offline, through direct mail, and more often through newer content and payment platforms (Over The Top TV,Amazon payments, Apple Pay, etc).  T&P management is typically difficult, if not impossible on these channels.  This makes it difficult to calculate cross-channel performance, as you're using multiple different mechanisms.

	3) It's time intensive to get the right access, and stay up to date -- If you have full control over every part of your web presence, it's straightforward and well documented to add in tags and pixel code.  However, many companies and organizations use a variety of different platforms, and a variety of different consultants to manage their communications.  Some platforms don't allow for custom javascript, some platforms are locked out because of permissions, etc.  Also, any change to any platform will require someone moderately technical to go update the T&P code -- which can quickly fall out of date.

	4) It keeps changing -- Similar to (4), the major T&P trackers out there are constantly tweaking and updating their interfaces and code to adapt to the web.  For example, Facebook keeps changing the name of their pixel conversion tracking --  as of this writing it's the Website purchase data, but was previously combinations of the website conversion and website purchase conversion data.

For these reasons, Frakture recommends source code based conversion tracking.

## Source Code based conversion tracking
Source code based tracking is another very common means of tracking performance.  While there are different names (utm_source,origin codes, tracking codes, etc, etc), the core idea is to attach a string of unique characters (e.g. DM_2020_EOQ2_Water_FNEIV2) to an outgoing message, and then carrying that code through the whole conversion process.

The major benefits of source code based conversion tracking are:

	1) It's channel agnostic -- Just about every means of modern communication can attach a code string to a message.  The practice started in direct mail

	2) It fails nicely -- Unlike some of the Native and T&P trackers based tools that may fail with no further information about why it failed, if you see an uncoded transaction, you can track down and fix where it came from.  It doesn't stop a transaction from going through, or depend on what platform you're using.

	3) There's no mucking with javascript, etc -- Almost every transaction processor natively supports attaching a source code to a transaction, WITHOUT coding, and carries that through to their reporting.

	4) It's widely understand -- You can have an intelligent conversation about source coding with marketers who have been in the industry for 30 years, or for 30 days.  It's that consistent, decade by decade.

Despite the pros, there are a couple of downsides:
	1) You HAVE to source code messages and links.  If you send out messaging without a source code, there's no easy way to pair up the conversions with that message.  You're effectively just not tracking conversions at that point.

	2) Your source codes need to be good, and unique - If you send the same source code out 10 time, there's no way to know how any given one of those codes performed.  Also, If you don't maintain a good list of what each source code means (EMEQ2 means Email, 2nd quarter), then you're limited on the insights you can derive for your messaging.  Good source code design is an ever evolving set of expertise -- at Frakture we've seen hundreds of different styles.

	3) You need to post-process your source codes for message performance -- If you want to know the performance of any given message, like a Facebook post or email, you need to do the work to pair up the messaging data (impressions, clicks, spend) with the conversions.  At Frakture we call this process "attribution".

##At Frakture
At Frakture we have built a huge amount of technology for Source Code based conversion tracking.  From generating unique, high quality, source codes, through attribution, through parsing out legacy codes, through deriving insight across channels, Frakture works on the whole process.  We try to take away the downsides of source code tracking, so you can focus on messaging, and not on configuring hunks of code in an obscure web technology.  While our Bots are capable of pulling T&P tracking data, the limits of that conversion tracking quickly becomes apparent as you use more and more technologies.

Use source code based conversion tracking -- it scales better than any other current mechanism.
