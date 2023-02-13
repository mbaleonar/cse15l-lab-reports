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
In 1821, [01;31m[KMexico[m[K declared its independence from Spain. Tension had been simmering for decades, fostered by Spain’s treatment of her New Spanish-born colonists, or criollos (deemed to be second-class citizens compared to those born in the homeland). Her trade laws decreed that everything produced in New Spain must first cross the Atlantic to Spain before being traded with a third country so that the proper taxes and tariffs could be collected. The geography of the northern Yucatán region separated it physically from the rest of New Spain, and fewer colonial landowners settled here than the area around the new capital (now [01;31m[KMexico[m[K City). Furthermore, this isolation led to the development of a strong independent streak for both colonists and indigenous peoples. The Yucatán declared its independence in 1821 but did not join the fledgling country of [01;31m[KMexico[m[K until 1823. In 1840, it changed its mind, and withdrew from the union. This was the catalyst for the oppressed Maya to take up arms against their colonial oppressors.
Meanwhile, under the presidency of Porfirio Diaz, Quintana Roo on the Yucatán peninsula’s eastern coast,  named after Andreas Quintana Roo — a writer and independence movement leader between 1810 and 1821 — was declared a territory of [01;31m[KMexico[m[K in 1902. Government troops clamped down on rebellious Indians, who continued to resist until a peace treaty was finally negotiated in 1935. The overthrow of Porfirio Diaz in 1917 led to reform and a new constitution, including a bill of rights for Mexican workers. Many haciendas were broken up and returned to the people. But the Yucatán remained a backwater, largely forgotten and ignored. No overland route existed from Mérida to the rest of [01;31m[KMexico[m[K until 1949, when the first railway arrived. Before then, all commercial travel to and from the peninsula was by sea, and it was faster and easier to travel to Cuba or the US than to [01;31m[KMexico[m[K City.
[01;31m[KMexico[m[K’s Mega-Resort
Despite its considerable oil reserves and mineral wealth, debt, booming population growth, and grinding poverty have crippled the economy of modern [01;31m[KMexico[m[K. In an effort to bring more hard currency into the country, the government decided to promote tourism. A three-year study of various sites was conducted by a consortium of government and private interests, and the deserted island of Cancún won out: not only was it a beautiful spot, but its use would revive the flagging economy of the Yucatán and finally bring Quintana Roo into the fold. The territory was eventually granted statehood in 1974, the same year that Cancún opened to the public.
Cancún is now [01;31m[KMexico[m[K’s most popular holiday destination, pulling in almost three million tourists each year. New roads have appeared, and televisions and refrigerators are now the norm in villages that didn’t even have electricity 20 years ago. Despite creating a pocket of wealth for the region, [01;31m[KMexico[m[K itself suffered a number of crises in the 1980s and 1990s, including a drastic devaluation of the peso in 1995 following months of economic chaos. The US extended 40 billion dollars in loans to stabilize the monetary system. However, confidence in the politicians is still low, and the 22% increase in the price of tortillas, the basic food of the people, in early 2000 indicates that the problems are not yet over.
These questions are for governments based in [01;31m[KMexico[m[K City, many miles from the Yucatán. A greater question for the region itself: Can the development be controlled? What was a deserted coastline two decades ago is now a bustling Riviera. Coral reefs are being damaged by careless divers; lagoons that once teemed with tropical fish are now being polluted by suntan lotion; the beaches where sea turtles once laid their eggs are being taken over by sun-beds and volleyball nets; crocodiles and manatees that once cruised the coastal waters are now endangered species. Conservation areas such as Rio Lagartos, in the north, give hope for the future, but conservationists lost one recent battle, when they were powerless to prevent the International Pier at Puerto Maya on Cozumel from being built directly on top of North Paradise Reef. Cancún — in fact the whole Yucatán peninsula — is embroiled in an important struggle, one that is being faced all over the world — the battle between the conflicting demands of development and conservation.
`
I ommited a few lines since there was still a lot of text, but essentially 
