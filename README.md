# Shakespeare Misattribution Investigation
Author: Drew Holcombe
______________________________________________________________________________________________________
## Overview 
The authorship of plays written during the Elizabethan period is poorly documented: uncredited collaborations were common, and publishers frequently misattributed work to the incorrect writer. As such, plays credited to Shakespeare were not always exclusively written by him: some may have been collaborations, or may have been revised by other writers. Using the text of plays known to have been written by Shakespeare and one of his contemporaries, Thomas Middleton, can one identify instances of potential collaboration using natural language processing?

## Business Problem

Plays written during Shakespeare's time, the Elizabethan period, are rarely documented clearly. Writing plays during this time looked more like writing films does today that it looks like writing novels or plays. It was common for writers to collaborate or revise others' work, and this was not always credited; for example, Shakespeare is known to have written works with John Fletcher, Thomas Middleton, and George Wilkins, both in some instances that were documented at the time and some when they were not. Historians and literary scholars have identified uncredited collaborations in the past based on writing style, handwriting, and other factors.

One play credited to Shakespeare that has been widely speculated, but never proven, to have been a collaboration is Timon of Athens. Many aspects of this play are unusual for Shakespeare: its writing style changes throughout the play, its tone is unusually cynical, and its conclusion is considered unsatisfying. This has drawn speculation of its authorship, but there is no documentation of the play being a collaboration.

The goal of my modelling process is to go through Timon of Athens line-by-line and identify possible sections that do not match Shakespeare's usual writing style using natural language processing. This can help modern historians and literary scholars flag sections of the text that can be analyzed more closely as being potentially misattributions.

## Data Overview

The [Shakespeare dataset](https://www.kaggle.com/datasets/kewagbln/shakespeareonline) contains the complete works of William Shakespeare, with each row containing a single line of dialogue, stage direction, or scene identification. The relevant columns to be used are "PlayerLine," containing the text, "Play," containing the play that line belongs to, and "ActSceneLine," which identifies the act, scene, and line number of each line of dialogue. Other columns containing information not useful to this problem are dropped.

The [Middleton datasets](https://tech.org/~cleary/middhome.html) (created manually due to the lack of stylistic formatting in their source), separated by play, also contain a line of dialogue in each row. These datasets do not contain stage directions or scene identifications: there is only one column, containing the text of each line.

The nine plays used in training the model contain 23,241 lines of dialogue in all. Lacking the text of "Michaelmas Term" and "A Mad World, My Masters," the model has less text from Middleton to train on than Shakespeare.

## Methods 
After working with multiple model types, the most successful model was a Multinomial Naive Bayes model with tuned hyperparameters.

## Results
The accuracy of my model in identifying unseen works attributed to either Shakespeare or Middleton was 78.6%, compared to the dummy classifier's accuracy of around 62%. The final model had a precision score of 78.1%, and a recall score of 90.7%.

The accuracy score of 78.6% is strong, but has room for improvement and skepticism while we interpret its findings. The other metrics tell us that the predictions will most likely over-predict Shakespeare as the writer of the bulk of the text.

## Conclusion

The model's predictions on test data confirms that it has a tendency to over-predict Shakespeare as the writer of unseen data over Middleton. Timon of Athens, however, is the only work attributed to Shakespeare from the set containing any window that the model attributes to Middleton. 

Most interestingly, in my opinion, is the section of Timon of Athens between lines 900 and 1400. This section, scenes 5 through 10 of the play, comes much closer to Middleton's word choice than the rest of the piece. This play also has very distinct changes in its predicted authorship compared to the other plays we've looked. Given the model's patterns we've discussed, this section is worth further investigation.

Overall, from this modelling process, we see a strong difference in the word choice of scenes five through ten of Timon of Athens compared to the rest of the piece, which points to the possibility that Middleton contributed to that section, especially considering the types of errors this model tends to make. However, at this point, the model does not firmly predict that Middleton wrote that section.

Some next steps I'd like to take to clarify these findings include training the model on additional Middletonian plays, such as "A Mad World, My Masters" and "Michaelmas Term," which I was not able to obtain in a usable format for this process. I'd also look into other proposed collaborators, such as George Chapman, and broadly continue working through the iterative modelling process. I'd also be interested in applying this process to other works with contested authorship to provide suggestions as to where historians and literary scholars can investigate more closely.

## For More Information

Please review my full analysis in my [Jupyter Notebook](./working_notebook.ipynb) or my [presentation](./presentation.pdf).

For any additional questions, please contact Drew Holcombe at drew.holcombe7@gmail.com.

## Repository Structure

```
├── README.md                                    <- The top-level README for reviewers of this project
├── Final_Notebook.ipynb                         <- Narrative documentation of analysis in Jupyter notebook
├── presentation.pdf                             <- PDF version of project presentation
├── data                                         <- Externally sourced project data
└── Graphs                                       <- Graphs created in working notebook
```
