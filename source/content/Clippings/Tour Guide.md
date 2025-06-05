---
title: "Tour Guide"
source: "https://cs.brown.edu/courses/cs019/2018/tour-guidetour-guide.html"
author:
published:
created: 2025-06-03
description:
tags:
  - "clippings"
---
#### Tour Guide

No doubt you remember the campus tour—  the walking backwards, the explanation of meal plans, the intramural sports speech.... It’s a fine tradition, but the admissions department is running out of willing volunteers. That’s where you come in: you’ve been asked to write a program to calculate tours for campus visitors.

##### 2 Overview

The Admissions Office has given you a set of map data that models Brown’s campus. Note that the map data contains many sites that are not tour stops, such as intersections and intermediate landmarks. All of the map locations, together with the paths between those locations, form a Graph. To go from one tour stop to another, your program should be able to find the shortest path from any point in this Graph to every other point in the Graph.

To do this, you will implement Dijkstra’s algorithm to compute the shortest paths between Graph locations. Each location on a Graph is at a specific position defined in Cartesian coordinates. This position will be represented as a Point:

> | data Point: |
> | --- |
> | \| point(x:: Number, y:: Number) |
> | end |

A Graph will represent each possible tour stop as a Place, which includes the name of a location, its position, and the location’s connected neighbors:

> | data Place: |
> | --- |
> | \| place( |
> | name:: Name, |
> | position:: Point, |
> | neighbors:: Set<Name>) |
> | end |

Every Place will have a unique, unambiguous Name; however, more than one Place may be located at the same Point. Also, all Graph representations of campus data must be bidirected and connected, and a Place cannot have itself as one of its neighbors.

To provide a rough estimate of the time it takes tour guides to walk around buildings, the Admissions Office has a particular way they would like you to calculate the “distance” between two Place s or Point s. They define the “distance” between two Place s or two Point s as the [Manhattan distance](https://en.wikipedia.org/wiki/Taxicab_geometry) between their Cartesian coordinates: that is, the “distance” between two points $(a_x, a_y)$ and $(b_x, b_y)$ is the sum of the absolute differences of their Cartesian coordinates:

$$
dist(a, b) = |a_x - b_x| + |a_y - b_y|
$$

You do not need to (and should not) write functions to do the Manhattan distance computation yourself, as the support code provides the following two functions:

- Place.distance:: Place -> Number This notation means that distance is a method on Place s.
	Given another Place, it returns the Manhattan distance between the two Place s.
- Point.distance:: Point -> Number
	Given another Point, it returns the Manhattan distance between the two Point s.

##### 3 Dijkstra’s Algorithm

Using the above data specifications, you will implement the following function:

> | dijkstra:: Name, Graph -> Set<Path> |
> | --- |

dijkstra You are welcome to work with lists within your program and convert the output to a set at the end. You may assume that converting a list to a set using list-to-set runs in $O([m \rightarrow m])$ time, where $m$ is the number of elements in the list.consumes a Name denoting the starting Place for your shortest-path search, and the Graph of possible tour stop locations. It should return a Set<Path> (where a Path is a List<Name>) that contains a Path for every Place in the Graph indicating the shortest total distance path from the starting location to that Place.

The locations in each path should be in the order in which they should be visited to get from the starting location to the last location in the path.

If the given name does not match any place in the graph, your program should reflect that there is no path to any places in the graph by returning the empty set.

Your dijkstra implementation should run in $O([s \rightarrow s \cdot \log s])$ time, where $s$ is the number of vertices in the graph. Note that a complete graph (with an edge between every pair of vertices) would have $(s \cdot (s−1))/2$ edges, making this impossible. However, graph representations of real maps are usually not so densely connected, and for your runtime analysis you may assume that each vertex has only some constant number of neighbors.

##### 4 Campus Tour

Due to recent surges in the number of prospective students, the Admissions Office would also like to consolidate their existing tours into a single “campus tour”. More precisely, they would like you to extend your program to be able to find a path through sets of predefined “tours”, such as an “Art Tour” or “Dorm Tour”.

We define a single tour as

> | data Tour: |
> | --- |
> | \| tour(title:: String, stops:: Set<Name>) |
> | end |

which records the title of a tour and the set of places that are visited on the tour.

Every Tour will have a unique, unambiguous title.

Using this data type, you will implement the following function:

> | campus-tour:: Set<Tour>, Point, Graph -> Path |
> | --- |

This consumes a set containing the tours to consolidate, a point representing the starting position for the tour on campus, and a graph representing campus locations. It should compute a path that visits each place in the provided set of tours. Assume that each stop in the given set of tours appears in the graph.

Observe that these Tours have no fixed order—  your program should choose the next place to visit by moving toward the closest, unvisited place in the provided set, even if this results in tours being interleaved. The “closest, unvisited place” should be determined using the Manhattan distance between the points where two places are located, not the path length between two places. Furthermore, it should move towards the closest, unvisited place using the shortest path possible.

Even if the name of a place appears in multiple tours, it only needs to be visited once. At the same time, regardless of whether or not a name appears in any of the supplied tours, it is also possible to visit a place more than once if necessary.

Also, since a tour guide might not start their tour exactly at the same point as a place in the graph, your campus-tour function should first find the site closest to the starting Point, and then continue to the nearest tour stop according to the specifications above.

Keep in mind that if you aren’t given any tours or the tours you are given contain no places to visit, you don’t have to go anywhere, so make sure your output reflects this. (There are no runtime requirements for campus-tour, but you will be asked to analyze the runtime of this function \[[Analysis](https://cs.brown.edu/courses/cs019/2018/#%28part._analysis%29)\].)

##### 5 Map Data

The map data for this assignment can be found [at this link](https://code.pyret.org/editor#share=1u_UPQ0Z2N867XQQqJkGDo5MFFS97yysX). This file is already imported in the provided code and testing stencils, so you do not need to copy this file yourself; it’s only provided here if you want to look at it. This file contains actual map data for Brown’s campus. You are welcome to play with the Brown data in the interactions window and use them in your tests. However,you should not use this data in your implementation because we might use different graphs when grading.

In this file, the following constants are provided to you:

- brown-university-landmarks:: Graph
	Represents all of the locations on the Brown campus map that your program will be processing. This may be used as an argument to dijkstra or campus-tour.
- brown-university-tours:: Set<Tour>
	A set of tours provided by the Admissions Office. This may be used as an argument to campus-tour.

##### 6 Support Code

The support definitions for this assignment can be found [at this link](https://code.pyret.org/editor#share=1hVLncE2-w5JjhSucmLJdVaoxNWEylPjX). Like the map data, this file is already imported in the provided code and testing stencils, so you do not need to copy this file yourself.

The support code contains definitions for all of the data types defined above, and also includes definitions for the following functions:

- to-graph:: Set<Place> -> Graph
	Returns a graph containing the places in the given set. You can use this function for the purposes of creating graphs for testing your functions, but you are not allowed to use to-graph to implement any required functionality.
- Graph.get:: Name -> Place Recall that this notation means this is a method.
	Given a name, returns the place in the graph that has that name. You may assume this function runs in time constant in the number of places in the graph.
- Graph.names:: -> Set<Name>
	Returns a set containing the names of all places in the graph. You may assume this function runs in time linear in the number of places in the graph.

##### 7 Testing

You may find writing tests for this assignment difficult at first. We strongly recommend drawing out example graphs by hand before writing tests to make sure that your understanding of the problem specification is correct (in particular, paying close attention to the Manhattan distance part of the specification).

Also, note that there may be multiple correct answers for dijkstra or campus-tour on certain graphs. You may wish to consider developing an is-valid function to verify that the properties of output from your functions are as expected.

##### 8 Analysis

You should also hand in a PDF analysis document addressing the following questions:

1. Analyze the worst-case running time of your dijkstra function. Show your work, as always!
2. Analyze the worst-case running time of your campus-tour function. Show your work, as always!
3. As is, your campus-tour always visits the nearest unvisited selected stop. Is this optimal? That is, does this algorithm create the shortest path visiting all the selected tour stops (in terms of Manhattan distance)? If so, explain why this is true. If not, provide a counter-example.
4. The distance function in this assignment is somewhat unconventional, but it is still compatible with Dijkstra’s algorithm. Consider the case where the Admissions Office requests a change to the Point.distance implementation so it uses a different distance function, such as Euclidean (straight-line) distance, spherical distance in latitude and longitude, etc. Does every possible distance function work with Dijkstra’s algorithm? If so, explain why this is true. If not, provide a counter-example. Assume that every function in the set of possible distance functions we are considering always returns a number given two points (that is, it does not raise an error).

##### 9 Built-Ins

In addition to the allowed functions in the general guidelines, you can also use immutable [string dictionaries](https://www.pyret.org/docs/latest/string-dict.html). To use string dictionaries, you will need to import them with the following lines of code:

> | import string-dict as SD |
> | --- |
> | type StringDict = SD.StringDict |

The StringDict methods .get, .get-value,.set, .has-key, .remove, and .count run in constant time in the number of entries in the StringDict.

.keys runs in linear time in the number of entries in the StringDict.

##### 10 Template Files

[Implementation](https://code.pyret.org/editor#share=1RvlKmzfqD2UfzJ32mCvH__b7Kslx9C3w&v=be0f222)

[Examplar](http://examplar.cs.brown.edu/editor#template=1NuRqymH6EmEHZcAyN-4fccifCyvc4sl_)