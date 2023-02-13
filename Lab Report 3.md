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
