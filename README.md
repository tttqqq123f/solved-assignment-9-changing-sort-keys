Download Link: https://assignmentchef.com/product/solved-assignment-9-changing-sort-keys
<br>
In <em><strong>week 8</strong></em>, we saw an example of a <strong>Student</strong> class that provided a static<strong>compare_strings_ignore_case()</strong>method. We needed to define such a method because our <em><strong>sort algorithm</strong></em>(which was in the <strong>StudentArrayUtilities</strong> (<strong>SAU</strong>) class) had to have a basis for comparing two<strong>Student</strong>objects, the foundation of <strong>SAU</strong>s sorting algorithm. Since a <strong>Student</strong> is a compound data type, not a<strong>float</strong> or a <strong>string</strong>, there was no pre-defined less-than, <strong>&lt;,</strong> operation available, so we created our own<strong>compare_strings_ignore_case()</strong>, which was based on the spelling of the <em><strong>last name</strong></em>. You can review those notes to see its definition.

We want to make the sort more flexible in this assignment. Sometimes we want to sort on <em><strong>last name</strong></em>, as we did in the lectures, but other times we may choose to sort on the <em><strong>first name</strong></em> (useful for informal communication) or <em><strong>total points</strong></em> (useful for analyzing statistics). We could go into the<strong>compare_strings_ignore_case()</strong> method and change its definition to work on <em><strong>first name.</strong></em> Or, we could rename it to <strong>compare_two_numbers()</strong> and base it on <em><strong>total points</strong></em> (or for that possibility just change<strong>SAU</strong>‘s<strong>float_largest_to_top()</strong> so that compare the points itself &lt; or &lt;=, no method call needed. But, such “solutions” only replace the inflexibility of <em><strong>last name</strong></em> with the inflexibility of some other criteria.

So here’s the plan: we will provide <strong><em>class</em> Student</strong> with a new <em><strong>class method</strong></em> s<strong>et_sort_key()</strong> which will establish a new sort criteria. A client will invoke it whenever it wants to switch to a new basis for comparison. The client will pass an argument to <strong>set_sort_key()</strong> telling it which one of the three<strong>Student</strong>attributes it wants future sort algorithms to use. The <strong>Student</strong> class will keep its<strong>compare_strings_ignore_case</strong>() <em><strong>static method</strong></em>, but add a new <em><strong>class method</strong></em>called<strong>compare_two_students()</strong>(which can use the older method as a helper). This name doesn’t commit to<strong>string</strong> vs. <strong>number</strong>, plus it gives the <strong>SAU</strong> class a unified method to invoke,<strong>Student.compare_two_students()</strong><em><strong>,</strong></em> inside its<strong>float_largest_to_top()</strong>. The current <em><strong>sort key</strong></em> will inform<strong>compare_two_students()</strong> how to make the comparison.

No Output (SAU class)

Another change we’ll make affects the output modality. Rather than displaying the array directly in the SAU class, we want to make the class “U.I. neutral.” So we will replace <strong>SAU</strong>‘s <strong>print_array()</strong> method with a<strong>to_string()</strong> method and let the client choose how to use that. In our example <strong><em>main program</em></strong> we will be sending the string array to the <em><strong>console</strong></em>.

Median (SAU class)

We’ll add one more <em><strong>class method</strong></em> to <strong>SAU</strong>: <strong>double get_median_destructive( cls, array, array_size)</strong>. This method will return the <em><strong>median</strong></em> of the <strong>total_toints</strong> values in an array. Look up <em><strong>median</strong></em>. It is defined as the “middle-value” and is easily computed, but you first have to sort the array in order to find it. Fortunately, you already have the sort method.

Client

Our client will declare <em>three <strong>Student</strong> arrays</em> to make sure our median works: one array that has an odd number of students (<em><strong>15</strong></em>), one that has an even number of students (<em><strong>16</strong></em>) and one that has a <em><strong>single student</strong></em>.

We’ll test the <strong>sort_key</strong> and sort algorithm only on the even numbered array, and then we will test our median computation on all three arrays.

The Program Spec

These changes should not be complicated as long as you read carefully and follow directions. New and modified members/methods are all very short, so stay focused and apply what you learned back in <em><strong>week 8</strong></em>.

<em>Additions</em> to the Student Class

We will add the following static members to the class in the modules.

static int consts:

<strong>SORT_BY_FIRST</strong> = 88

<strong>SORT_BY_LAST</strong> = 98

<strong>SORT_BY_POINTS</strong> = 108

These are the three <em><strong>sort keys</strong></em> that will be used by the client and the class, alike, to keep track of, or set, the <em><strong>sort key</strong></em>.   If the client wants to establish a new <em><strong>sort key</strong></em>, it will pass one of these tokens (say<strong>Student.SORT_BY_FIRST</strong>) to the setter described next.    I have intentionally made the literal values non-contiguous so you would not rely on their particular values in your logic.   You should be able to change the values without breaking your program (but you don’t have to change them; use the three values above).

static int:

<strong>sort_key</strong> – this will always have one of the three constants above as its value. Make sure it initially has<strong>SORT_BY_LAST</strong> in it, but after the client changes it, it could be any of the above constants.

You should supply the following simple <strong><em>class methods</em></strong>:

<strong>def set_sort_key(cls, key)</strong>: — a <em><strong>mutator</strong></em> for the member <strong>sortKey</strong>.

<strong>def get_sort_key(cls):</strong> — an <em><strong>accessor</strong></em> for <strong>sortKey</strong>.

A new class comparison method:

<strong>def compare_two_students(cls, first_stud, second_stud)</strong>:– This method has to look at the <strong>sort_key</strong> and compare the two <strong>Students</strong> based on the currently active<strong>sort_key</strong>. It will return a number as follows:

If <strong>sort_key</strong> is <strong>SORT_BY_FIRST</strong> it will use the two students’ <strong>first</strong> members to make the comparison. It will do this by passing those two values to <strong>compare_strings_ignore_case()</strong>, and “passing up” the returned value directly to the client.

If <strong>sort_key</strong> is <strong>SORT_BY_LAST</strong> it will use the two students’ <strong>last</strong> members to make the comparison. It will do this by passing those two values to <strong>compare_strings_ignore_case()</strong>, and “passing up” the returned value directly to the client.

If <strong>sort_key</strong> is <strong>SORT_BY_POINTS</strong> it will use the two students’ <strong>total_points</strong> members to make the comparison. It will do this by subtracting the second student’s points from the first student’s points and returning that number.

Notice that whatever value the current <strong>Student.sort_key</strong> has, <strong>Student.compare_two_students()</strong> returns a value value that’s negative if <strong>first_stud</strong> “comes <em>before</em>” <strong>second_stud,</strong> positive if <strong>first_stud</strong> “comes<em>after</em>“<strong>second_stud</strong> and 0 if they are the same <strong>–<em>– interpreted through the current value of sort_key</em></strong>. (It doesn’t matter what the the exact value returned besides its being +, – or 0.)

<em>Change</em> to the StudentArrayUtilities Class

<strong><em>Replace</em> print_array() with to_string().</strong> Generate the same kind of <strong>string</strong>, but instead of sending it to the screen, return it to the client.

<strong><em>Adjust</em> float_largest_to_top()</strong> to call <strong>compare_two_students()</strong> rather than<strong>compare_strings_ignore_case()</strong>. Make adjustments required by this change.

Add a <em><strong>class method</strong></em> <strong>get_median_destructive(cls, array, array_size):</strong> – This computes and returns the <strong><em>median</em></strong> of the total scores of all the students in the array The details are simple, but you have to take them each carefully:

Dispose of the case of a one-element array. A one-element array returns its one and only<strong>Student</strong>‘s<strong>total_points</strong>. (This case can actually be skipped if you handle the next cases correctly, but it doesn’t hurt to do it separately, here.)

<strong>Even-numbered arrays &gt;= 2</strong> elements: find the two middle elements and return their average of their total points.

<strong>Odd-numbered arrays &gt;= 3</strong> elements: return the total points of the exact middle element.

<strong>Special Note</strong>: This method has to do the following. It must <strong><em>sort the array</em></strong> according to <strong>total_points</strong>in order to get the medians, and that’s easy since we already have the sort method. Then it has to find the middle-student’s score (e.g., if the array is size <strong>21</strong>, the middle element is the score in<strong>array[10]</strong>, <em>after the sort</em>). But, before doing the sort, it also has to change the <strong>sort_key</strong> of the <strong>Student</strong>class to <strong>SORT_BY_POINTS</strong>. One detail, that you may not have thought of, is that, at the very start of the method, it needs to save the <strong><em>client’s sort key</em></strong>. Then, before returning, restore the client’s sort key. This method doesn’t know what that sort key might be, but there is an accessor <strong>get_sort_key()</strong>that will answer that question.

This method has the word “<strong>Destructive</strong>” in its name to remind the client that it may (and usually will) modify the order of the array, since it is going to sort the array by <em><strong>total points</strong></em> in the process of computing the <em><strong>median</strong></em>. However, it will not destroy or modify the client’s <strong>sort_key</strong> when the method returns to client (see previous bullet).

If the user passes in a bad <strong>arraySize</strong> (&lt; 1) return a 0.

The Main Program

Our client will declare <em>three <strong>Student</strong> arrays</em>: using direct initialization, as in the modules: no user input. The array sizes should be 15, 16 and 1. The second array can be the same as the first with one extra<strong>Student</strong>tagged onto the end. Each array should be initialized in no particular order: unsorted in all fields.

Using the largest, even numbered, array:

display the array immediately before calling a sort method,

sort the array using the default (initial) <em><strong>sort key</strong></em> and display,

change the <em><strong>sort key</strong></em> to <em><strong>first name</strong></em>, sort and display,

change the <em><strong>sort key</strong></em> to <em><strong>total score</strong></em>, sort and display,

<strong>set_sort_key()</strong> to <em><strong>first name</strong></em>, call the <strong>get_median_destructive()</strong> method and display the <strong><em>median score</em></strong>. and finally

call <strong>get_sort_key()</strong> to make sure that the <strong>get_median_destructive()</strong> method preserved the client’s <strong>sort_key</strong> value of <em><strong>first name</strong></em> that was just set prior to the <strong>get_median_destructive()</strong> call.

Using each of the two other arrays:

get the median of each array and display. No other testing needed in this part.

Here’s a sample output, but you must not use my arrays. Make your own as per the spec above.

<pre>Before default sort (even): ----------     name: smith, fred    total points: 95. ----------     name: bauer, jack    total points: 123. ----------     name: jacobs, carrie    total points: 195. ----------  ... etcAfter default sort (even):  ----------     name: bauer, jack    total points: 123. ----------     name: cassar, john    total points: 321. ----------     name: charters, rodney    total points: 295. ----------     name: jacobs, carrie    total points: 195. ... etcAfter sort BY FIRST:  ----------     name: renquist, abe    total points: 148. ----------     name: jacobs, carrie    total points: 195. ----------     name: loceff, fred    total points: 44. ----------     name: perry, fred    total points: 225.  ... etcAfter sort BY POINTS:  ----------     name: loceff, fred    total points: 44. ----------     name: smith, fred    total points: 95. ----------     name: zz-error, trevor    total points: 108. ----------     name: bauer, jack    total points: 123. ----------  ... etcMedian of even class =   ...Successfully preserved sort key.Median of odd class = ... Median of small class = ...</pre>