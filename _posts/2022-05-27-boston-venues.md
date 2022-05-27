---
layout: post
title: "Boston Music Scene Tangent: Adding Venues from the Phoenix to Wikidata"
categories:
---

One of my dweebiest hobbies is adding music venues to Musicbrainz and Wikidata, and in looking through the concert listings from the [4 August 1989 issue of the _Boston Phoenix_](https://archive.org/details/sim_boston-phoenix_august-04-10-1989_18_31/page/n87), I was struck by what a nice, structured source of venue data newspaper listings provide! Maybe not structured enough to extract it automatically (lots of OCR issues to clean up, for one thing; changing formats over time, for another[^1]), but enough to make copying over the names, street addresses, and cities of venues into a spreadsheet a pleasant and relaxing data entry task, if you're into that sort of thing.[^2]

So we go from this: 

<img src="/bg-in-boston/assets/boston_phoenix_1989-08-04/s3_p25_friday_venues.png" alt="Friday concert listings from section 3, page 25 of The Boston Phoenix (Volume 18, Issue 31)" >

to this:

<table style="display: block; overflow-y: scroll; max-height: 300px">
  {% for row in site.data.boston_venues_1989_08_04 %}
    {% if forloop.first %}
    <tr>
      {% for pair in row %}
        <th>{{ pair[0] }}</th>
      {% endfor %}
    </tr>
    {% endif %}

    {% tablerow pair in row %}
      {{ pair[1] }}
    {% endtablerow %}
  {% endfor %}
</table>

Once you have that basic table of venues, you can move into [OpenRefine](https://openrefine.org/) and start reconciling against Wikidata. A few of these venues already had associated Wikidata items (thanks largely, I would assume, to the [Boston Rock City edit-a-thon](https://www.wikidata.org/wiki/Wikidata:WikiProject_Linked_Data_for_Production/Arthur_Freedman_Collection_Project) last year). But based on the music listings from this single issue of the Boston Phoenix, I ended up [adding 42 venues to Wikidata](https://editgroups.toolforge.org/b/OR/7097365728c/). 

I want to go back and do some further research on each of these, in particular to get their dates of opening and closure, if possible. We do know that each of these would have been open in August 1989, at least, and I'm not sure what the best way to capture that is. I only semi-recently[^6] learned the term [floruit](https://en.wikipedia.org/wiki/Floruit), which has an [associated Wikidata property](https://www.wikidata.org/wiki/Property:P1317). Does it make sense to use floruit for a building and/or a business? It does to me![^3] Looking at [what types of items in Wikidata are currently using the floruit property](https://w.wiki/5BLD): yes, it's predominantly used for humans, but there are also organizations in there. 

There is also the tricky question of modeling organizations vs the buildings from which they operate in Wikidata--[WikiProject Performing arts](https://www.wikidata.org/wiki/Wikidata:WikiProject_Performing_arts/Data_structure/Data_modelling_issues#Items_confounding_architectural_structures_and_organizations) has a whole section on this in their documentation. Using [instance of](https://www.wikidata.org/wiki/Property:P31) [music venue](https://www.wikidata.org/wiki/Q8719053) for the items I've been creating is probably not ideal from that perspective, but not quite sure what would be better.

For example, we can dig into the history of 533 Washington Street. At some point this address has been associated with:

- Geo. A. Plummer & Company (ladies' and children's specialty garment house)
    - [Advertisment in a publication from 1895](https://books.google.com/books?id=MF567gJot54C&pg=PA63)
    - [Advertisement in October 1896 issue of Wellesley Magazine](https://books.google.com/books?id=LLUAAAAAYAAJ&newbks=1&newbks_redir=0&printsec=frontcover&pg=PT2)
    - [Advertisement (also targeting Wellesley students) from 1897](https://books.google.com/books?id=7bUQAAAAYAAJ&pg=PT17)
- Adams House Restaurant 
    - [Matchcover, ca. 1940-1975](https://ark.digitalcommonwealth.org/ark:/50959/9593v464p)[^5]
    - [Scanned menu](https://www.reddit.com/r/VintageMenus/comments/6k7o0v/adams_house_restaurant_533_washington_street/)
        -  No date, but can probably infer from the prices: when would it have made sense for a full course luncheon to cost $1.10?
- Hub Club
    - [1989 NY Times article](https://www.nytimes.com/1989/04/06/garden/currents-new-york-primitivism-in-boston.html) announcing Hub Club's opening in the 1866 Singer Sewing Machine building
    - [OpenCorporates entry for Hub Club](https://opencorporates.com/companies/us_ma/042895285) stating that it dissolved in 1998
    - And a [semi-relevant item from Northeastern's special collections](https://repository.library.northeastern.edu/files/neu:276398) - proposal (or announcement?) of event series at the Hub Club targeting the "professional Hispanic clientele in the Massachusetts area"
- Felt
    - [2002 Boston Business Journal article](https://www.bizjournals.com/boston/stories/2002/11/25/newscolumn10.html)
    - [Felt homepage as of 23 November 2002](https://web.archive.org/web/20021123084339/http://www.feltboston.com:80/)
    - Tribe Nightclub at Felt: lesbian club within the venue? Or just a lesbian night held at Felt?
        - [Yelp reviews from 2007 to 2008](https://www.yelp.com/biz/tribe-nightclub-felt-boston)
        - [Archived Tribe website](https://web.archive.org/web/20070404191431/http://www.tribenightclub.com/thursday_info.htm)
 
 And as of 2016, there was a [plan to replace the building with high-rise apartments](https://www.bostonglobe.com/business/2016/05/29/pencil-tower-project-would-threaten-opera-house-owners-say/3tWxisLIPE3ey7pcBPp2EJ/story.html), but not sure how that's going or what ended up happening. 

In theory, you'd want Wikidata items for each distinct building at 533 Washington Street, as well as items for the distinct organizatons occupying those buildings. Right now, though, [Hub Club](https://www.wikidata.org/wiki/Q111823878) is the only one in there, so there isn't as much of a structural need to distinguish between the building and the business.

Anyway, let's end this with the current state of Massachusetts music venues in Wikidata:
<iframe style="border: none; width: 100%; height: 300px;" src="https://query.wikidata.org/embed.html#%23title%3A%20Music%20venues%20in%20Massachusetts%0A%23defaultView%3AMap%7B%22markercluster%22%3A%22true%22%7D%0A%0ASELECT%20%3Fmusic_venue%20%3Fmusic_venueLabel%20%0A%28group_concat%28distinct%20%3FlocationLabel%3B%20separator%3D%22%3B%20%22%29%20as%20%3Flocations%29%20%0A%28sample%28%3Fcoords%29%20as%20%3Fcoords%29%20%0AWHERE%20%7B%0A%20%20%20hint%3AQuery%20hint%3Aoptimizer%20%22None%22.%0A%20%20%20%20%3Fmusic_venue%20wdt%3AP131%2B%20wd%3AQ771%3B%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP31%2Fwdt%3AP279%2a%20wd%3AQ8719053%3B%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP131%20%3Flocation.%0A%20%20%20%20OPTIONAL%7B%3Fmusic_venue%20wdt%3AP625%20%3Fcoords%7D%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20%0A%20%20%20%20%20%20%20%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%0A%20%20%20%20%20%20%20%20%3Flocation%20rdfs%3Alabel%20%3FlocationLabel.%0A%20%20%20%20%20%20%20%20%3Fmusic_venue%20rdfs%3Alabel%20%3Fmusic_venueLabel.%7D%0A%7D%20group%20by%20%3Fmusic_venue%20%3Fmusic_venueLabel" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

---

[^1]: The [11 January 2002 issue](https://archive.org/details/sim_boston-phoenix_january-11-17-2002_31_2/), for example, has this very helpful [club directory](https://archive.org/details/sim_boston-phoenix_january-11-17-2002_31_2/page/n46/mode/1up).

[^2]: Some more thoughts on this: coming from a computer science background, there's a weird shame I feel about _not_ automating processes or using programmatic solutions. But in a task like this, which no one is asking me or paying me to do, and there's not really any urgency involved, why should I feel that? Manually entering data can be a meditative task that makes you engage with and learn about individual entities, in a way that you couldn't at scale--efficiency isn't always be the goal.

[^3]: It would also help with some public art modeling for a separate project. If you know from a historic photo or whatever that a mural was up during a given period, but don't have documentary evidence for its installation or removal date, you could potentially use that date as the floruit?

[^5]: This was my first and completely accidental encounter with the [Boston Public Library's matchbook cover collection](https://www.digitalcommonwealth.org/collections/commonwealth:9593v3679)--what a good resource for researching historical businesses and events that I just never would have thought of looking into.

[^6]: I wish I could remember more of the context now, but I think there was a conference presentation at some point in the past two years on using floruit not in the literal "flourishing" sense but as a better-than-nothing estimate of when a person was alive when birth and death dates are unknown. 