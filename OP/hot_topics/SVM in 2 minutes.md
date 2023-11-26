> from 'Visually Explained' on [youtube](https://www.youtube.com/watch?v=_YPScrckx28&t=1s)

Elegant Method for classification.

SVM draws an hyperplane so that all the points of one category stay on one side and all the others in the other side.
All the data are represented as points in the space where the axis are the attributes.

There could be many hyperplanes, but the one we want is the one that maximizes the distance to point in either category, which is called the margin.
The data points on the margin are called supporting vectors.
![[Pasted image 20231122235013.png|400]]

The Convex Optimization Problem is the following
![[Pasted image 20231122235108.png|400]]

In many applications the points cannot be separated with hyperplanes, but we can add artificial attributes computed from existing ones to find a plane.
The [Kernel Trick](https://www.youtube.com/watch?v=Q7vT0--5VII) allows to performe these steps in a very efficient manner.

![[Pasted image 20231122235306.png|400]]

# Kernel Trick
---

[Kernel Trick](https://www.youtube.com/watch?v=Q7vT0--5VII) 