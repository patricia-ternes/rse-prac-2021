# Problem 6

You have been approached by a Social Sciences researcher who wishes to collect some data from Twitter and Facebook to follow the comments posted by a particular group of individuals in the run-up to the 2019 Indian general election.

How would you go about the process of **Requirements Analysis** for this query? What are the most important questions you should ask, and why?

## Solution

Before defining the software project is necessary to proper understand specifically what the research wants. So my first step must be a deeper investigation about the real goal and about the challenges to fulfil them. In other words,  process. For instance, some initial questions should be answered:

> About the final product:

- The research wants the software or just the data?
- If the research wants the software, what is the desired language? Is it necessary a GUI?

These questions would help pre-select a group of tools to solve the problem.

> About the data:

- What information does the researcher need?
- Is there any ethics implications or guidelines for this project?
- Is it possible to collect these information from Twitter and Facebook? (from a technical and ethical point of view)
- What particular group is the researcher interested in? How to select this group among the other users?
- Is it necessary to collect information from other users (to use as benchmarking)?
- In total, how many individuals will be considered?
- Data from Facebook need to be consistent with Twitter data (same variables)?
- How to deal with missing information?
- Any specific recommendation for data type?

As the data involve real individuals, special attention must be given to ethical factors. These questions seek to elucidate both the ethical factor and provide an understanding of what the researcher is looking for. Furthermore, it is important to understand what the researcher is looking for so as not to collect data that will not be necessary for the research.

> About the data storage:

- How should collected information be organised and stored? What is the preferred output format?
- Facebook and Twitter data are going to be stored in the same file?
- How to deal with same users data from both platforms?
- Will the collected data need to be processed? Although data processing is a later process, it may be necessary to ensure the anonymity of users (which requires some initial processing).
  - will users be anonymized?
  - a unique user identifier must be generated?
  - should any variables be separated into categories (age bands, for example)?
  - should any variable be unified with another (age and sex, for example)?
- If the data is not anonymized, are there any special requirements for data storage?

These questions would help to identify the requirements for the output.

