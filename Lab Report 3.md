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

`$ grep --color=always "Mexico"  travel_guides/berlitz2/Cancun-History.txt `

![image](https://user-images.githubusercontent.com/122484639/218533290-41afba32-6385-4873-bbc4-82ea243d350b.png)

The `--color` command highlights the searched text in red for ease of access, so the user doesn't have to scour a particulary long line for the exact text. This is especially usefuly for when looking for a specific usage of a command in a java file or such.

I was curious to see what would happen when the included highight was included when exporting the `grep` search into a txt file, and this was the result:

`  $ grep --color=always "Mexico"  travel_guides/berlitz2/Cancun-History.txt > grepHighlight.txt`

`These people’s ancestors arrived in Central America many thousands of years ago. Small bands of Asiatic hunters migrated across the Bering Strait land bridge before 12,000 b.c. and gradually spread southwards through the Americas. During the Archaic period (after 5,200 b.c.), these people settled in what is now modern [01;31m[KMexico[m[K. They developed a primitive agriculture, domesticating cattle and cultivating corn, beans, chili peppers, and squash (a pumpkin-like vegetable) in burned clearings in the jungle. Over time, a society developed that was so successful they could devote time to activities other than simple food cultivation. These people, known as the Olmec, are considered to be the first Mesoamerican culture, the one from which all others evolved. They developed a calendar based on a 52-year cycle. They also constructed pyramids for worship.
Grijalva’s stories focused Spanish attention on central [01;31m[KMexico[m[K, and in 1519 Hernan Cortés landed in Veracruz, to start an expedition that would end in the conquest of Moctezuma and the Aztec Empire. Though he had begun his campaign without the King’s authority, once news of the treasures captured by Cortés reached Madrid, a royal warrant was dispatched to legitimize the victory and create “New Spain” — the latest Spanish colony. However, it was left to Don Francisco de Montejo, “a gentleman of Seville,” following in the great conquistador’s wake, to take possession of the Yucatán in the name of the Spanish king.
In 1821, [01;31m[KMexico[m[K declared its independence from Spain. Tension had been simmering for decades, fostered by Spain’s treatment of her New Spanish-born colonists, or criollos (deemed to be second-class citizens compared to those born in the homeland). Her trade laws decreed that everything produced in New Spain must first cross the Atlantic to Spain before being traded with a third country so that the proper taxes and tariffs could be collected. The geography of the northern Yucatán region separated it physically from the rest of New Spain, and fewer colonial landowners settled here than the area around the new capital (now [01;31m[KMexico[m[K City). Furthermore, this isolation led to the development of a strong independent streak for both colonists and indigenous peoples. The Yucatán declared its independence in 1821 but did not join the fledgling country of [01;31m[KMexico[m[K until 1823. In 1840, it changed its mind, and withdrew from the union. This was the catalyst for the oppressed Maya to take up arms against their colonial oppressors.`

I ommited a few lines since there was still a lot of text, but as observed, the previously red colored text is nested with grep's own formatting for color, which seems to not translate well into a plain text file. Doesn't seem to be particularly useful, but at the very least it still technically highlights which word was found.

For both of these problems I used 
