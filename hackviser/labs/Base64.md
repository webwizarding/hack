# Cryptanalysis
Encoding techniques Base64

---

## Challenge

Base64 is a encoding algorithm that allows you to transform any characters into an alphabet which consists of Latin letters, digits, plus, and slash. Thanks to it, you can convert Chinese characters, emoji, and even images into a “readable” string, which can be saved or transferred anywhere.

What is the decoded message of the text that has been encoded using Base64 inside the file?

file: `TW9uYUxpc2FEYVZpbmNp`

---

## First and only step
Revert the string through the base64 format 

```
Base64: "TW9uYUxpc2FEYVZpbmNp"
Decoded: "MonaLisaDaVinci"
```

---

# Flag
```
MonaLisaDaVinci
```
