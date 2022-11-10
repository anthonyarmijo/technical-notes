https://www.markdownguide.org/cheat-sheet/

Tags
#bluepill 
#redpill

Italic. As you're typing and you want to *emphasize something*, you add asterisks.

Bold. Typically, I'll use this when I want to bring attention to **Big Nouns** ^2ad5a6

* Lists.
* Lists

- [ ] CMD + Enter to add a checklist or cross it out

## Footnotes
This is a footnote [^1], and this is a longer footnote. [^bignote]

# Hash Tag (with Space) to Create Headers

## 2 Hashtags for L2 Headers

### 3 Hashtags for L3 Header
#### 4 Hashtags for L4 Headers
##### L5 Headers
###### L6 Headers

# Links 101
## Backlinking
* Adding a hashtag to a backlink allows you to reference a specific header on that page. [[Markdown Reference#Hash Tag with Space to Create Headers]]
* You can link any specific block of text using ^ : [[Markdown Reference#^2ad5a6]]
* You can also add a pipe to change the display text of the backlink [[Markdown Reference | Custom Backlink]]

## Websites
* Manually type out URL for normal hyperlink: https://www.google.com
* You can change the display text of a URL by using brackets followed by parenthesis [My Link](https://www.google.com)

# Code
`Use backticks to use inline code`

```

Use 3 backticks in a row for a code block.

```

As seen below, you can add a language code immediately after the first set of backticks. Visit this link to see supported languages and their respective codes: 
https://prismjs.com/#supported-languages

```powershell
Get-ADUser -Identity aarmijo
```

**Bash Example**
```bash
#!/bin/bash  
: '  
The following script calculates  
the square value of the number, 5.  
'  
((area=5*5))  
echo $area9
```

[^1]: Simple footnote
[^bignote]: Footnote with multiple paragraphs and code.
			Indent paragraphs to include them in the footnote.
			
			`{ my code }`
			
			Add as many paragraphs as you like.


