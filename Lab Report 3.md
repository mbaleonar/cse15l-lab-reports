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

`  mbale@Matt MINGW64 ~/Downloads/Java Files/skill-demo1-server/skill-demo1-data/written_2 (main)
  $ grep --color=always "Mexico"  travel_guides/berlitz2/Cancun-History.txt
  
  These people’s ancestors arrived in Central America many thousands of years ago. Small bands of Asiatic hunters migrated across the Bering Strait land bridge before 12,000 b.c. and gradually spread southwards through the Americas. During the Archaic period (after 5,200 b.c.), these people settled in what is now modern Mexico. They developed a primitive agriculture, domesticating cattle and cultivating corn, beans, chili peppers, and squash (a pumpkin-like vegetable) in burned clearings in the jungle. Over time, a society developed that was so successful they could devote time to activities other than simple food cultivation. These people, known as the Olmec, are considered to be the first Mesoamerican culture, the one from which all others evolved. They developed a calendar based on a 52-year cycle. They also constructed pyramids for worship.
Grijalva’s stories focused Spanish attention on central Mexico, and in 1519 Hernan Cortés landed in Veracruz, to start an expedition that would end in the conquest of Moctezuma and the Aztec Empire. Though he had begun his campaign without the King’s authority, once news of the treasures captured by Cortés reached Madrid, a royal warrant was dispatched to legitimize the victory and create “New Spain” — the latest Spanish colony. However, it was left to Don Francisco de Montejo, “a gentleman of Seville,” following in the great conquistador’s wake, to take possession of the Yucatán in the name of the Spanish king.
  ...
  `
  The `--color` command highlights the 
