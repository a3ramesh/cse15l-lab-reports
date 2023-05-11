My name is Advait Ramesh, and this is a lab report for Week 6 of Spring 2023 CSE 15L with Joe Politz. The goal of this lab report is to take the grep command and explore the different ways in which it can be used. 

Use 1: -c

The "grep" command can be used with "-c" in order to list the count of the lines that match a query, rather than listing the lines themselves. Here's an example:
```
[cs15lsp23sf@ieng6-202]:Alcohol_Problems:401$ grep -c "drug" Session3-PDF.txt 
4
```
In this case, it searched through the entire Session3-PDF.txt file looking for the word "drug." It only found 4 lines that contain the word "drug," so it printed out the number 4.

Here's another example:
```
[cs15lsp23sf@ieng6-202]:Env_Prot_Agen:406$ grep -c "carbon" section-by-section_summary.txt
2
```
In this case, it searched through the entire section-by-section_summary.txt file looking for the word "carbon." It only found 2 lines that contain the word "carbon," so it printed out the number 2.

This command to look at the number of lines that match a query is especially useful because if a text contains a large number of lines that match a query, it may fill up the entire screen, while listing the number of lines does not fill up the entire screen yet still gives the user a sense of the relevance of the term in the text. 

Use 2: -i

The "grep" command can be used with "-i" for the purpose of ignoring case; when searching for lines that match a query, the case of the letters in the query does not matter. Here is an example:

```
$ grep -i "where" section-by-section_summary.txt 
Administrator will not require a separate CEMS for each unit where
withdrawn from the opt-in provisions is where the unit qualifies as
for a declining price auction where winning bidders purchase
matter and carbon monoxide emissions. Where there is a modification
```
Notice that it printed the lines containing both "where" and "Where." This was because I typed "-i" after the grep command to indicate ignoring case.

Here is another example:
```
$ grep -i "drug" Session3-PDF.txt 
and his or her drinking or drug abuse and may be more motivated to
in a trauma center reported acceptance of referral for drug or
for practice and policy. Contemporary Drug Problems
role of alcohol and other drugs-an EAST position paper prepared by
Mental Health Services Administration. Alcohol and Other Drug
drugs: an assessment of testing and clinical practices in U.S.
```
Notice that it printed the lines containing both "drug" and "Drug." This was also due to typing "-i" after the grep command to indicate ignoring case.

This is a useful function because it saves time; the user doesn't have to type each individual version of the word if they want to get the full occurrence of the word in the text. Keep in mind that this function also applies to very long words or phrases, and it applies to when words are written in all-caps as well, making it all the more useful.

Use 3: -w

The grep command can also be used with "-w" for the purpose of only including lines that contain the individual word query itself, not also lines that contain words with a part of it that is the word query. Here is an example:
```
[cs15lsp23sf@ieng6-202]:911report:462$ grep -c "plan" chapter-1.txt
75
[cs15lsp23sf@ieng6-202]:911report:463$ grep -c -w "plan" chapter-1.txt
3
[cs15lsp23sf@ieng6-202]:911report:466$ grep -w "plan" chapter-1.txt
```
I used the -c command from earlier to make things less tedious. Notice how without the -w there are 75 lines that match, but with the -w there are only 3. This is because in the first case it counted all the lines that contained the sequence of letters 'p'-'l'-'a'-'n', not necessarily just the word "plan." In the second case, it only included the lines that contained the word "plan" in them.

Here is another example:
```
[cs15lsp23sf@ieng6-202]:biomed:479$ grep -c  "issue" rr74.txt
3
[cs15lsp23sf@ieng6-202]:biomed:481$ grep  "issue" rr74.txt
        lung nervous tissue [ 4, 5, 7, 8]. Thus, all three NOS
          Frozen lung tissue was homogenized in ice cold 750 μl
        species and tissue specific. Previous studies of NOS
[cs15lsp23sf@ieng6-202]:biomed:480$ grep -c -w  "issue" rr74.txt
0
```
Notice how when the query is "issue," there are 3 lines that match, but in all of those cases the matched word is not "issue," but "tissue." When we use "-w" with "issue," there are 0 lines that match, meaning that there are no occurrences of the word "issue."

This is a useful function as well because it saves time and energy; without this function, searches for a particular word would be misleading when they say a word appears in the text when it in fact does not. The use of this function saves the user's time in that they won't have to skim a text to find out if their query really yielded the results they wanted.

Use 4: -A, -B, -C

The grep command can be used with -A in order to print a certain amount of lines after the line containing the query. The grep command can also be used with -B in order to print a certain amount of lines before the line containing the query. Lastly, the grep command can be used with -C in order to print a certain amount of lines both before and after the line containing the query. Here is an example:

```
[cs15lsp23sf@ieng6-202]:biomed:496$ grep -A 2 "tissue" rr74.txt
        lung nervous tissue [ 4, 5, 7, 8]. Thus, all three NOS
        isoforms could contribute to modulation of pulmonary
        vascular tone. Studies using knockout mice for each of
--
          Frozen lung tissue was homogenized in ice cold 750 μl
          radioimmunoprecipitation assay (RIPA) buffer (1×PBS, 1%
          Igepal CA-630, 0.5% sodium deoxycholate, 0.1% SDS) plus
--
        species and tissue specific. Previous studies of NOS
        expression in systemic and pulmonary endothelial cells from
        different species in cultures [ 31, 32, 33, 34, 35, 36, 37]
```
Notice how it prints each line containing the query word "tissue" followed by the two lines right after it. 

Here is another example with -B:
```
[cs15lsp23sf@ieng6-202]:Alcohol_Problems:503$ grep -B 3 "drug" Session3-PDF.txt 
the medical condition or injury prompting admission provides a
"window of opportunity" when the individual may be more vulnerable
and more open to seeing the connection between current consequences
and his or her drinking or drug abuse and may be more motivated to
--
program in Texas described above demonstrated a 100% successful
referral to alcoholism treatment for patients and families who
agreed to be in the program.21 A substance abuse consultation team
in a trauma center reported acceptance of referral for drug or
--
injuries, and dangerous behaviors-and the revolving emergency
department door. J Trauma 1990;30:1252-8.
12. Soderstrom CA, Cole FJ, Porter JM. Injury in America: the
role of alcohol and other drugs-an EAST position paper prepared by
--
Protocol (TIP), No. 16. Rockville (MD): Department of Health and
Human Services; 1995. DHHS Publication No. (SMA) 95-3014.
40. Soderstrom CA, Dailey JT, Kerns TJ. Alcohol and other
drugs: an assessment of testing and clinical practices in U.S.
```
Notice how it prints each line containing the query word "tissue" with two lines preceding it. 

This is a useful function because it enables the user to get some within which their query word is used; this is a more efficient way to get the context behind each use of a certain word that does not involve printing out the entire text and scrolling to each use of that word. 

This concludes my lab report.





