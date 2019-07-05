## Relational Strategies in Customer Service (RSiCS) Dataset

Human-computer data from three live customer service Intelligent Virtual Agents (IVAs) in the domains of travel and telecommunications were collected, and reviewers marked all text that was deemed unnecessary to the determination of user intention. After merging the selections of multiple reviewers to create *highlighted* texts, a second round of annotation was done to determine the classes of language present in the highlighted sections such as the presence of Greetings, Backstory, Justification, Gratitude, Rants, or Emotions. This resulting corpus is a valuable resource for improving the quality and relational abilities of IVAs.


### Data

Data was collected from four sources.  The conversation logs of three commercial customer service IVAs and the Airline forums on TripAdvisor.com during August 2016.

Dataset numbering used in files:

1. TripAdvisor.com airline forum
2. Train travel IVA
3. Airline travel IVA
4. Telecommunications support IVA


#### Sanitation

The commercial data was sanitized to protect the identity of the companies and their customers.  No sanitation was needed for the TripAdvisor data as it is already publicly viewable on the forum.


##### Personal Identifiable Information

Personal Identifiable Information (PII) present in the commercial datasets have been removed by a manual two-pass review.  All numerical characters contained in PII such as telephone numbers, account numbers, confirmation or case numbers, etc have been replaced with \#'s.  Similarly, all other characters contained in PII such as names and addresses were replaced with -'s.  The original length of the requests is therefore preserved as this may be a useful feature in analysis.

Example:

*I cant sign into my account __1234__ with my user name __johndoe__*

becomes

*I cant sign into my account **\#\#\#\#** with my user name __-------__*


##### Company Origin

In order to publicly release the commercial data we agreed to anonymize it's source.  Company names were replaced with `cname-*` and product names with `pname-*`.

Example:

*Can I sign up for an **Airline** **clubname** perks card?*

becomes

*Can I sign up for an **cname--** **pname---** perks card?*


##### Re-identification

While it may be possible that an instance of PII was overlooked or to deduce the company of origin for a dataset, doing so violates the terms of use for this data.  By downloading or using this dataset for any reason you agree to not attempt any type of re-identification.


### File Contents and Formatting

####*x*\_*y*\_align.csv####
Alignment of reviewer __x__ to all other reviewers in their group for dataset __y__.


Columns:

+ **Reviewer A ID**:  __x__
+ **Reviewer B ID**:  Reviewer that the alignment score with __x__ is calculated against.
+ **Group ID**:  The group of 4 reviewers that the compared users belong to.
+ **Dataset ID**:  Dataset __y__ that the request originated from.
+ **Request ID**:  Unique ID of a request to allow joining between different files.
+ **Text**:  The original request text.
+ **Reviewer A Text**:  The request text with selections from reviewer A contained within [ and ].
+ **Reviewer B Text**:  The request text with selections from reviewer B contained within [ and ].
+ **Length**:  The character length (`n`) of the original request text in column 6.
+ **Error**:  The number of character positions (`e`) where the binary determination of A and B do not agree.
+ **Alignment Score**:  The alignment as calculated by `align = (n - e) / n`.
+ **Agreement**:  Whether or not A and B agree that *any* selection is necessary.


####all\_data\_by\_threshold.csv####
All requests with selections merged by threshold.  Each request is repeated 4 times, once for each merging threshold.

Columns:

+ **Dataset ID**:  Dataset that the request originated from.
+ **Group ID**:  The group of 4 reviewers that the selections originated from.
+ **Request ID**:  Unique ID of a request to allow joining between different files.
+ **MultiIntent**:  1 if at least one reviewer flagged the text as containing more that one user intention, 0 otherwise.
+ **Threshold**:  The threshold (`i`) to merge selections by.
+ **MergedSelections**: If at least `i` reviewers marked a character as unnecessary then it will be contained within the selected portion denoted by [ and ].
+ **Unselected**:  All text from **MergedSelections** not contained by [ and ].
+ **Selected**: All text from **MergedSelections** contained by [ and ].
+ **Removed**: Amount of text removed from the original request by the merged selections: `length(Selected) / n`



####tagged\_selections\_by\_sentence.csv####
Second annotation pass tagging relational language present in selections made by first pass of annotation.  Only contains requests in __all\_data\_by\_threshold.csv__ not marked as MultiIntent.

Columns:

+ **Dataset ID**:  Dataset that the request originated from.
+ **Group ID**:  The group of 4 reviewers that the selections originated from.
+ **Request ID**:  Unique ID of a request to allow joining between different files.
+ **Threshold**:  The threshold (`i`) to merge selections by.
+ **MergedSelections**: If at least `i` reviewers marked a character as unnecessary then it will be contained within the selected portion denoted by [ and ].
+ **Unselected**:  All text from **MergedSelections** not contained by [ and ].
+ **Selected**: All text from **MergedSelections** contained by [ and ].
+ **Greeting**: If a greeting of some kind (*Hi*, *How are you*) is present in **Selected**
+ **Backstory**: If self-exposure language is present in **Selected**.  The user is telling the audience about themselves, their situation, what led them to contact the agent or ask their question.
+ **Justification**: If justification language is present in **Selected**.  The user is giving facts to build credibility that their request or statement is true.   Also can be *why* they need resolution or a consequence if something is not resolved.
+ **Rant**: If ranting is present in **Selected**.  Excessive complaining or negative narrative.
+ **Gratitude**: If some expression of gratitude to the audience for past or future help is present in **Selected**.
+ **Other**: If some or all of the highlighted section does not contain any relational language in **Selected**.  Could be additional facts the user gave but reviewers determined was unnecessary to determine their intention, or a general question such as *Can you help?*.
+ **Express Emotion**: If any emotional language not covered by **Rant** is present in **Selected**


####all\_multi\_intent.csv####
All requests flagged as containing multiple intentions by at least one reviewer.  Useful for developing multiple intent detection strategies.

Columns:

+ **Dataset ID**:  Dataset that the request originated from.
+ **Group ID**:  The group of 4 reviewers that the selections originated from.
+ **Request ID**:  Unique ID of a request to allow joining between different files.
+ **Text**:  The original request text.
+ __Reviewer *x*:__  Will be `1` if reviewer __x__ believed more than one intent was present in the text, `0` otherwise.


### Terms of Use

This RSiCS dataset is made freely and publicly available under the [Open Database License](http://opendatacommons.org/licenses/odbl/1.0/) with the additional conditions:

+ Data has been sanitized to remove PII and origination of the IVAs.  Any attempt to re-identify individuals or sources of commercial IVA data is prohibited.  By downloading or using this dataset for any reason you agree to not attempt any type of re-identification.
+ Any publication created with use of this data must cite the paper: [bibTex](https://s3-us-west-2.amazonaws.com/nextit-public/rsics_arxiv.bib)


### Download

By downloading this dataset you agree to the Terms of Use declared above.

[rsics_dataset.tar.gz](https://s3-us-west-2.amazonaws.com/nextit-public/rsics_dataset.tar.gz)