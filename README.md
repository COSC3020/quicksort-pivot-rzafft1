[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=12093761&assignment_repo_type=AssignmentRepo)
# Quicksort Pivots

in the lectures I only briefly mentioned strategies for determining a good pivot
for quicksort. The implementation on the slides simply picks the leftmost
element in the part of the array that we consider as a pivot. I also mentioned a
few other ways of picking a good pivot, e.g. randomly.

Median-of-three is also a good way of picking a pivot -- inspect the first,
middle, and last elements of the part of the array under consideration and
choose the median value. Using the probabilities for picking a pivot in a
particular part of the array (in the same way as we did on slide 34), argue
whether this method is more or less (or equally) likely to pick a good pivot
compared to simply choosing the first element. Assume that all permutations are
equally likely, i.e. the input array is ordered randomly.

<ins>Initial Thoughts</ins>

**Picking leftmost element**
  1. We always pick the first element (could be anything). 
  2. Problem? If the array is sorted or almost sorted, this isnt greated
     
**Picking 'Median-of-three' element**
  1. We pick the median value of the first, mid, and last elements. In worst case scenarios (sorted list) this is an improvment from picking the leftmost runtime
  2. Problem? Comparing the first, mid, and last runs at constant time, this is not really a problem

Hypothesis : The goal for choosing a pivot, is to have the resulting partition divide the list into roughly equal halfs. Choosing a median value between the first, mid, and last element should, on average, have a better chance at dividing the list into rougly equal halfs, than always picking the first element. Deciding between three values in comparison to always picking one value should give us a better chance at placing the pivot near the middle of the list. 

Your answer must derive probabilities for choosing a good pivot and
quantitatively reason with them.

- lets say we divide our array into three parts (BAD PIVOT AREA , GOOD PIVOT AREA, BAD PIVOT AREA) and lets write out every possible tripple pivot combination. We will express each pivot option with a 'P'.
- if a pivot combination has a pivot in the 'GOOD PIVOT AREA' we can declare that it is a 'good' pivot, otherwise, there is not a 'good' pivot in the combination

```
- (PPP,_,_)  // BAD   
- (_,_,PPP)  // BAD   
- (PP,_,P)   // BAD     
- (P,_,PP)   // BAD  
- (P,P,P)    // GOOD  
- (_,PPP,_)  // GOOD  
- (PP,P,_)   // GOOD  
- (P,PP,_)   // GOOD  
- (_,PP,P)   // GOOD  
- (_,P,PP)   // GOOD  

the probabilites we want to look at are ...

- (P,P,P)    // GOOD : 1/4 * 1/2 * 1/4 = 2/64 * 6 = 3/16
- (_,PPP,_)  // GOOD : 1/2 * 1/2 * 1/2 = 8/64 * 1 = 2/16
- (PP,P,_)   // GOOD : 1/4 * 1/4 * 1/2 = 2/64 * 6 = 3/16
- (P,PP,_)   // GOOD : 1/4 * 1/2 * 1/2 = 4/64 * 3 = 3/16
- (_,PP,P)   // GOOD : 1/2 * 1/2 * 1/4 = 4/64 * 3 = 3/16
- (_,P,PP)   // GOOD : 1/2 * 1/4 * 1/4 = 2/64 * 6 = 3/16

some of these cases are the same so we can reduce these cases to ...

- (P,P,P)              // GOOD : 1/4 * 1/2 * 1/4 = 2/64 * 6 = 3/16
- (_,PPP,_)            // GOOD : 1/2 * 1/2 * 1/2 = 8/64 * 1 = 2/16
- (PP,P,_) or (_,P,PP) // GOOD : 1/4 * 1/4 * 1/2 = 2/64 * 6 = 3/16
- (P,PP,_) or (_,PP,P) // GOOD : 1/4 * 1/2 * 1/2 = 4/64 * 3 = 3/16

add up all the probabilities (3/16 + 2/16 + 3/16 + 3/16) to get total of 11/16
```

- Probability for choosing a 'good' pivot is ($100 \cdot \frac{11}{16}$) $68.75$ %.
- Therefore, my hypothesis was correct, the median of three pivot will have a better probability of selecting a pivot near the middle of the list, that the left most pivot selection
 

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.
