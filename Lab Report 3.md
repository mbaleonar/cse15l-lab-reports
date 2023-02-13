## CSE 15L Lab Report 3
# Researching Commands
---

## `grep`

For this lab I decided to go with `grep` to research. The four interesting command-line options I chose are as follows:

- `--color`
- `-v`
- `-n`
- `-C num`

---

## `--color`

I noticed that the `grep` results in the remote server included a color highlight of the serchable word, and I was curious if the option for highlighting was an external addon, and much to my delight I learned that the option was simply a prefixed command for `grep`.
The first example I have of using the `--color` exam was the following:

>$ grep --color=always "Mexico"  travel_guides/berlitz2/Cancun-History.txt 
>
>![image](https://user-images.githubusercontent.com/122484639/218533290-41afba32-6385-4873-bbc4-82ea243d350b.png)

The `--color` command highlights the searched text in red for ease of access, so the user doesn't have to scour a particulary long line for the exact text. This is especially usefuly for when looking for a specific usage of a command in a java file or such.

I was curious to see what would happen when the included highight was included when exporting the `grep` search into a txt file, and this was the result:

> ` $ grep --color=always "Mexico"  travel_guides/berlitz2/Cancun-History.txt > grepHighlight.txt`

>These people’s ancestors arrived in Central America many thousands of years ago. Small bands of Asiatic hunters migrated across the Bering Strait land bridge before 12,000 b.c. and gradually spread southwards through the Americas. During the Archaic period (after 5,200 b.c.), these people settled in what is now modern [01;31m[KMexico[m[K. They developed a primitive agriculture, domesticating cattle and cultivating corn, beans, chili peppers, and squash (a pumpkin-like vegetable) in burned clearings in the jungle. Over time, a society developed that was so successful they could devote time to activities other than simple food cultivation. These people, known as the Olmec, are considered to be the first Mesoamerican culture, the one from which all others evolved. They developed a calendar based on a 52-year cycle. They also constructed pyramids for worship.
>Grijalva’s stories focused Spanish attention on central [01;31m[KMexico[m[K, and in 1519 Hernan Cortés landed in Veracruz, to start an expedition that would end in the conquest of Moctezuma and the Aztec Empire. Though he had begun his campaign without the King’s authority, once news of the treasures captured by Cortés reached Madrid, a royal warrant was dispatched to legitimize the victory and create “New Spain” — the latest Spanish colony. However, it was left to Don Francisco de Montejo, “a gentleman of Seville,” following in the great conquistador’s wake, to take possession of the Yucatán in the name of the Spanish king.
>In 1821, [01;31m[KMexico[m[K declared its independence from Spain. Tension had been simmering for decades, fostered by Spain’s treatment of her New Spanish-born colonists, or criollos (deemed to be second-class citizens compared to those born in the homeland). Her trade laws decreed that everything produced in New Spain must first cross the Atlantic to Spain before being traded with a third country so that the proper taxes and tariffs could be collected. The geography of the northern Yucatán region separated it physically from the rest of New Spain, and fewer colonial landowners settled here than the area around the new capital (now [01;31m[KMexico[m[K City). Furthermore, this isolation led to the development of a strong independent streak for both colonists and indigenous peoples. The Yucatán declared its independence in 1821 but did not join the fledgling country of [01;31m[KMexico[m[K until 1823. In 1840, it changed its mind, and withdrew from the union. This was the catalyst for the oppressed Maya to take up arms against their colonial oppressors.

I ommited a few lines since there was still a lot of text, but as observed, the previously red colored text is nested with grep's own formatting for color, which seems to not translate well into a plain text file. Doesn't seem to be particularly useful, but at the very least it still technically highlights which word was found.
For both of these examples I used the [Linux Manual Page](https://man7.org/linux/man-pages/man1/grep.1.html) to find the implementation of `--color`.

---

# `-v`

`-v` functions like the inverse of a standard `grep` search, outputting every line that *doesn't* include the searched phrase.</b>
Here's an example of such a search:

>`$ grep --color=always -v  "Mexico"  travel_guides/berlitz2/Cancun-History.txt`
>   
>



>A Brief History  
>During the last fifty years, a great deal of research has been undertaken to discover more about the great ancient societies of the Yucatán. Huge sections of their daily lives (and particularly why they came to abandon their cities) are still shrouded in mystery, but great strides have been made in deciphering their hieroglyphs and stelae (inscribed stone pillars). Despite these mysteries, there are few places in the world where the past feels as close as it does in the Yucatán. The thatched huts that appear in 1,000-year-old carvings at Uxmal can be seen today in every roadside village. The stone metates, or grinding dishes, which grace many a kitchen in town or village, are identical to those left as offerings to the rain gods in centuries past. Away from the cities, the people still speak the Mayan tongue, and their religious beliefs still bear the imprint of the ancient rituals of their ancestors. And, perhaps most striking of all, the distinctive hooked nose and sloping forehead of the ancient Maya, whose stony profiles look down on the visitor from the carved walls of their ruined cities, are still reflected in the features of the local people.   
>The Maya  
>By 1500 b.c. the group that came to be known as the Maya settled in an area which stretched from the Pacific coast to the southern Yucatán, taking in modern-day Guatemala, Belize, the western parts of El Salvador and Honduras, and the Mexican state of Campeche. In the succeeding centuries they migrated into the northern Yucatán — what are now the modern Mexican states of Yucatán, Quintana Roo, and part of Tabasco.

(As previously mentioned I still omitted the rest of the output text). As one can see, it's a little difficult to see if the inverted search worked or not since we have no way to see the relative position of the lines or which lines the omitted word originally was (spoiler alert, we have a solution of that with the next command option). This is still quite useful since there will be times where one would want to search for everything *but* the specified phrase, sort of like prepending a "-" symbol on a google search to narrow down a search.

I was curious to see what would happen when I would add something incredibly vague like "a" which has a lot of usage in vocabulary, so I went ahead and did that.

>`$ grep --color=always -v  "a"  travel_guides/berlitz2/Cancun-History.txt  `
>
>
>
>
>A Brief History  
>The Henequen Boom
>
>

The result was as much as I expected, although I didn't include case-sensitivity so the title line survived the mass exodus of the second most used vowel in the english language. Clearly this doesn't have any sort of practical usage, but in a similar vein as the first example, it does help narrow down unwanted searches.  
For both of these examples I used the [Linux Manual Page](https://man7.org/linux/man-pages/man1/grep.1.html) to find the implementation of `-v`.

---   

# `-n`

Now, was there a way to help visualize where the lines of text are in the searched file? Yes, there is. With the helpful `-n` command, the outputted search gets prepended with the line number for easy reference. Combined with the `--color` command, this outputs some really useful information at a glance.   
Here's the first example of its usage:   

>`$ grep --color=always   "people" -n travel_guides/berlitz2/Cancun-History.txt`
>![image](https://user-images.githubusercontent.com/122484639/218544385-e2d4aa28-3bd4-4458-8d36-a6542bab1507.png)


I changed up the search to `"people"`, but as seen in the other examples there was a paragraph with that word, which seems to have been line 6. The `--color` effect on `-n` seems to be green for the line numbers, which does help to differenciate it from the rest of the text.   

I also did an example using `-v` to see if empty lines also get shown with their line number. Here's the result:   

>`$ grep --color=always  -v "people" -n travel_guides/berlitz2/Cancun-History.txt`
>![image](https://user-images.githubusercontent.com/122484639/218546004-a6c2ad70-e3b9-4f56-bb59-e2446718938f.png)

And yes, it does seem that 


