---
layout: post
title: "Boston Music Scene Tangent: Adding Venues from the Phoenix to Wikidata"
categories:
---

So, one of my dweebiest hobbies is adding music venues to Musicbrainz and Wikidata, and in looking through the concert listings from the [4 August 1989 issue of the _Boston Phoenix_](https://archive.org/details/sim_boston-phoenix_august-04-10-1989_18_31/page/n87), I was struck by what a nice, structured source of venue data newspaper listings provide! Maybe not structured enough to extract it automatically (lots of OCR issues to clean up, for one thing; changing formats over time, for another[^1]), but enough to make copying over the names, street addresses, and cities of venues into a spreadsheet a pleasant and relaxing data entry task, if you're into that sort of thing.

Once you have that, you can move into [OpenRefine](https://openrefine.org/) and start reconciling against Wikidata. A few of these venues already had associated Wikidata (thanks largely, I would assume, to the [Boston Rock City edit-a-thon](https://www.wikidata.org/wiki/Wikidata:WikiProject_Linked_Data_for_Production/Arthur_Freedman_Collection_Project) last year).

Based on the music listings from this single issue of the Boston Phoenix, I ended up [adding 42 venues to Wikidata](https://editgroups.toolforge.org/b/OR/7097365728c/). 

I want to go back and do some further research on each of these, in particular to get their dates of opening and closure, if possible. We do know that each of these would have been open in August 1989, at least, and I'm not sure what the best way to capture that is. I only semi-recently learned the term [floruit](https://en.wikipedia.org/wiki/Floruit), which has an [associated Wikidata property](https://www.wikidata.org/wiki/Property:P1317). I wish I could remember more of the context now, but I think there was a conference presentation on using floruit not in the literal "flourishing" sense but as a better-than-nothing estimate of when a person was alive when birth and death dates are unknown. 

Does it make sense to use floruit for a building and/or a business? It does to me (it would also help with some unrelated public art modeling--i.e., if you know from a historic photo or whatever that a mural was up during a given period, but don't have documentary evidence for its installation or removal date). Looking at [what types of items in Wikidata are currently using the floruit property](https://w.wiki/5BLD): yes, it's predominantly used for humans, but there are also organizations in there. 

There is also the tricky question of modeling organizations vs the buildings from which they operate in Wikidata--[WikiProject Performing arts](https://www.wikidata.org/wiki/Wikidata:WikiProject_Performing_arts/Data_structure/Data_modelling_issues#Items_confounding_architectural_structures_and_organizations) has a whole section on this in their documentation. Using instance of music venue for the items I've been creating is probably not ideal from that perspective, but not quite sure what would be better.

For example, we can dig into the history of 533 Washington Street--now, there's an apartment complex there, but apparently this used to be the Singer 

- At some point this was New Adams House Restaurant 
- Hub Club
    - [1989 NY Times article](https://www.nytimes.com/1989/04/06/garden/currents-new-york-primitivism-in-boston.html) announcing Hub Club's opening in the 1866 Singer Sewing Machine building
    - [OpenCorporates entry for Hub Club](https://opencorporates.com/companies/us_ma/042895285) - dissolved in 1998
    - [Semi-relevant item from NUASC](https://repository.library.northeastern.edu/files/neu:276398) - proposal (or announcement?) of event series at the Hub Club targeting the "professional Hispanic clientele in the Massachusetts area"
- In 2002 this became Felt https://www.bostonherald.com/2010/06/25/felt-to-be-rechristened-as-sin/
- In 2010 this became Sin? https://www.bostonherald.com/2010/06/25/felt-to-be-rechristened-as-sin/
- [2016 - Downton Crossing's Tall New Towers, Mapped](https://boston.curbed.com/maps/downtown-crossing-new-towers-mapped)


The current state of Massachusetts music venues in Wikidata:
<iframe style="border: none; width: 100%; height: 300px;" src="https://query.wikidata.org/embed.html#%23title%3A%20Music%20venues%20in%20Massachusetts%0A%23defaultView%3AMap%7B%22markercluster%22%3A%22true%22%7D%0A%0ASELECT%20%3Fmusic_venue%20%3Fmusic_venueLabel%20%0A%28group_concat%28distinct%20%3FlocationLabel%3B%20separator%3D%22%3B%20%22%29%20as%20%3Flocations%29%20%0A%28sample%28%3Fcoords%29%20as%20%3Fcoords%29%20%0AWHERE%20%7B%0A%20%20%20hint%3AQuery%20hint%3Aoptimizer%20%22None%22.%0A%20%20%20%20%3Fmusic_venue%20wdt%3AP131%2B%20wd%3AQ771%3B%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP31%2Fwdt%3AP279%2a%20wd%3AQ8719053%3B%0A%20%20%20%20%20%20%20%20%20%20wdt%3AP131%20%3Flocation.%0A%20%20%20%20OPTIONAL%7B%3Fmusic_venue%20wdt%3AP625%20%3Fcoords%7D%0A%20%20%20%20SERVICE%20wikibase%3Alabel%20%7B%20%0A%20%20%20%20%20%20%20%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%22.%20%0A%20%20%20%20%20%20%20%20%3Flocation%20rdfs%3Alabel%20%3FlocationLabel.%0A%20%20%20%20%20%20%20%20%3Fmusic_venue%20rdfs%3Alabel%20%3Fmusic_venueLabel.%7D%0A%7D%20group%20by%20%3Fmusic_venue%20%3Fmusic_venueLabel" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups" ></iframe>

[^1]: The [11 January 2002 issue](https://archive.org/details/sim_boston-phoenix_january-11-17-2002_31_2/), for example, has this very helpful [club directory](https://archive.org/details/sim_boston-phoenix_january-11-17-2002_31_2/page/n45/)