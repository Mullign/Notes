Throughout this chapter, we have deliberately chosen to illustrate the interplay between individual preferences, collective welfare, game theory, and algorithms through examples with which most of us have daily experience, such as driving, shopping, or reading news. But there are many more specialized settings in which algorithmic game theory has long played a central role in highly consequential decisions.

One such setting is broadly known as _matching markets_ in economics. While this phrase may bring to mind dating apps like Coffee Meets Bagel, matching markets are usually found in much more formal scenarios in which we want to pair up individuals with each other, or individuals with institutions. One long-standing application area is medical residency hiring, in which the approach we'll describe is implemented as the National Resident Matching Program (NRMP, affectionately known as "The Match").

The basic problem formulation is as follows. Candidates for medical residences each have an individual ranking of potential programs. For example, suppose the candidates Elaine and Saeed have the following ranked list of residences (ignore the annotating characters for now, which we will discuss shortly):

|Elaine|Saeed|
|---|---|
|_Harvard_|_Cornell_|
|_Johns Hopkins_|_UC San Diego @_|
|_UC San Diego &_|_Harvard #_|
|_Baylor_|_Johns Hopkins_|

Based on application materials and interviews, the schools of course also have their own ranked list of candidates, such as:

|Harvard|UC San Diego|
|---|---|
|_Saeed #_|_Roger_|
|_Elaine_|_Saeed @_|
|_Roger_|_Elaine &_|
|_Gwyneth_|_Mary_|

So this is a two-sided market -- candidates and hospitals -- and there are also capacity constraints, because each candidate can of course take only one residency, and each hospital can only take a limited number of residents (which for simplicity we'll assume is also just one). Thus, as with dating and commuting, we once again have a large system (many thousands of applicants, and hundreds of schools) of interacting, competing preferences and would like to specify a desirable solution -- and a fast algorithm for finding one.

Let's approach the notion of a desirable solution by first specifying what we _don't_ want to happen. Consider candidates Elaine and Saeed in the example above. Suppose we match Elaine with UC San Diego (indicated by the "&" characters next to both), and Saeed with Harvard (indicated by the "#" characters next to both). Then regardless of any other matches we make, this solution is _unstable_, because Saeed prefers UC San Diego to Harvard, and UC San Diego prefers Saeed to Elaine -- that is, the match indicated by the "@" characters would be preferable to both Saeed and UC San Diego, compared to their respective outcomes under the & and # matches. So while Elaine and Harvard might be happy, Saeed and UC San Diego have an incentive to deviate or defect from their assigned matches (Harvard and Elaine, respectively) and hook up with each other instead. A solution in which there are no such potential defections is called a stable matching. A matching with this property is not at risk of unraveling as students and hospitals iteratively defect from their proposed matches.

A stable matching is conceptually quite similar to a Nash equilibrium, but now two parties (a candidate and a medical school) must jointly defect to a mutually preferred outcome, due to the two-sided nature of the market. And like a Nash equilibrium, a stable matching in no way promises that everyone will be satisfied with the outcome: a candidate assigned to her 117th-favorite hospital may not be happy, but as in a Nash equilibrium, there is nothing she can do about it, because the 116 hospitals she prefers already have candidates they like better than her. Candidates and hospitals that are paired together in a stable matching are stuck with each other. Nevertheless, a stable matching is an intuitive solution to such pairing or assignment problems -- certainly any solution that is _not_ a stable matching is vulnerable to defections and is therefore problematic -- and it is a _Pareto optimal_ solution as well, in the sense that there is no way to make anyone better off without making someone else worse off (similar to the accuracy-fairness Pareto curves discussed in Chapter 2).

Like other topics in this chapter, stable matchings have both a long history and fast algorithms for comptuing them, going back at least to the seminal 1962 work of David Gale and Lloyd Shapley. The so-called Gale-Shapley algorithm is sufficiently simple that it even has a plain English description on Wikipedia, whimsically phrased as pairing men and women via traditional Victorian courtship:

- In the first round, _a)_ each unengaged man proposes to the woman he prefers most, and then _b)_ each woman replies "maybe" to her suitor that she most prefers and "no" to all other suitors. She is then provisionally "engaged" to the suitor she most prefers so far, and that suitor is likewise provisionally engaged to her.
    
- In each subsequent round, _a)_ each unengaged man proposes to the most-preferred woman to whom he has not yet proposed (regardless of whether the woman is already engaged), and then _b)_ each woman replies "maybe" if she is currently not engaged or if she prefers this suitor over her current provisional partner (in this case, she rejects her current provisional partner who becomes unengaged). The provisional nature of engagements preserves the right of an already-engaged woman to "trade up" (and, in the process, to "jilt" her until-then partner).
    
- This process is repeated until everyone is engaged.
    

The Gale-Shapley algorithm has two very nice properties. First, regardless of the preferences, everyone gets matched (if there are equal number of men and women, and they don't deem any of their potential partners as absolutely unacceptable; for instance, every medical student wants to do a residency no matter what). Second, the matching computed by the algorithm is stable in the sense we described above. Algorithms generalizing to the cases where there are unequal numbers of men and women (or students and medical schools), or where one side of the market can accept more than one partner (as in medical residences), also exist. These algorithms are in widespread practical use, including in assigning actual medical residencies and other competitive admissions settings, such as matching students to public high schools and matching pledges to sororities in universities. (In contrast, US undergraduate college admissions are generally done in a much more haphazard fashion, giving rise to experiments in admissions office gamesmanship such as early decision, early action, requiring standardized tests or not, additional essays, and the like -- all to the exhaustion and frustration of applicants and their parents.)

One of the most striking applications of algorithmic matching in the real world -- one that literally has saved human lives -- is to the problem of paired kidney donation. Many people with kidney disease die every year while awaiting a transplant donor, and the problem is exacerbated by the fact that the blood type of a donor must be compatible with that of the recipient to be biologically viable (there are also a variety of other medical compatibility constraints). We can view the blood type and biology of a donor as a form of "preferences" over recipients -- a donor "prefers" to donate to compatible recipients, and not to incompatible ones. Similarly, a recipient prefers to receive a transplant from a compatible donor.

While there are many details that make this problem more complicated than medical residency matching, there are again practical, scalable algorithms that maximize the efficiency of the solution found, where here efficiency means maximizing the total number of compatible transplants that occur globally -- ideally across all hospitals, not just within a single one. For his algorithmic and game-theoretic insights on this problem (and the others we have mentioned, including the medical residency match) and his efforts to convince the medical community and hospitals that it was worth the effort to pool their transplant donors, recipients of data, Alvin Roth was awarded the 2012 Nobel Prize in economics -- along with the aforementioned Lloyd Shapley, whose early work initiated the era of algorithmic matching.

**This excerpt was taken from** _**The Ethical Algorithm: The Science of Socially Aware Algorithm Design**_ **by Michael Kearns and Aaron Roth.**

Kearns, M., & Roth, A. (2020). _The ethical algorithm: The Science of Socially Aware Algorithm Design_. Oxford University Press.