### Auto-Parsing Source Codes

Frakture enriches the source code dictionary by having bots parse your full source code string for the detail they contain.

For example, from a hypothetical code *EOQ_FB_TX*, you might need to mark out that this is part of the End Of Quarter campaign ("EOQ"), representing a Facebook message ("FB") targeted to the state of Texas ("TX"). If you commonly write your source codes with a consistent syntax along these lines -- "Campaign_Channel_Targeting", in this example -- Frakture can train the bots to recognize that syntax and automatically extract these three [source code elements](enrichment/source_code_elements "Source Code Elements") from your codes.

In the real world, there's usually lots of different source codes for an organization, both legacy and new source codes, that don't necessarily all follow the same format. That's okay. Frakture can read multiple different syntaxes, known as "source code formats", to extract meaning from different source codes.
<div style="float:right; width:250px; padding:4px; background-color:#E8E8E8"><div style="position:relative; width:250px; float:right;" align=center>Sometimes different codes express the same concept (for example, "Facebook Ads") with different code characters (for example, "FB" or "ADS" or the full word "Facebook" or a purely abstract signifier like "12"). No problem! Frakture has a labels dictionary that we can use to link all these concepts together, so that our reports' totals understand them all to denote a single common channel.</div></div>
These source code formats define what the source code looks like, typically using regular expressions or simplified merge fields. Our example code above might be read by a source code format such as *{{campaign}}_{{channel_prefix}}_{{geo}}*, but as a Frakture user you don't need to worry about writing our hieroglyphs. We'll work with you to get things sorted.

What _is_ important is that your common formats, however many there might be, are recognizably distinct from one another. "Campign_Channel_Targeting" -- three elements connected by underscores -- looks a lot like "Appeal_Fund_Goal". Ideally, robot-friendly source codes will have either or both of these characteristics:

* A predictable sequence of [source code elements](enrichment/source_code_elements "Source Code Elements") (the same elements, in the same order) divided by a predictable separating character such as a hyphen or an underscore. Our "Campign_Channel_Targeting" code above is a good example.

* A string of letters or numbers with a predictable length, where characters in specified sequential positions (for instance, the third letter of the code, the fourth through sixth letters of the code, and then the seventh and eighth letters of the code) are reserved to signal a source code element. For example, *21FEOQTX*.

During auto-parsing, Frakture will go through the different formats and attempt to use them to parse the source code. The results will be stored in your [Source Code Dictionary](enrichment/source_code_dictionary "Source Code Dictonary"), along with the format match that keyed those results. You as the human manager always retain the ability to override manually these automated results.
