
# Calculating Distance Lab

### Introduction

In this lab, you will write methods to calculate the distance of various neighbors from each other.  Once again, let's assume that the $x$ coordinates represent avenues of a neighbor, the $y$ coordinates represent streets.  We will also assume that the distance between each street and the distance between each avenue is the same.

We will work up to a function called `nearest_neighbors` that given a neighbor, finds the other neighbors who are closest.

### Getting Started

Let's declare a variable `neighbors` and assign it to a list of dictionaries, each representing the location of a neighbor.


```python
neighbors = [{'name': 'Fred', 'avenue': 4, 'street': 8}, {'name': 'Suzie', 'avenue': 1, 'street': 11}, 
             {'name': 'Bob', 'avenue': 5, 'street': 8}, {'name': 'Edgar', 'avenue': 6, 'street': 13},
             {'name': 'Steven', 'avenue': 3, 'street': 6}, {'name': 'Natalie', 'avenue': 5, 'street': 4}]
```


```python
# __SOLUTION__ 
neighbors = [{'name': 'Fred', 'avenue': 4, 'street': 8}, {'name': 'Suzie', 'avenue': 1, 'street': 11}, 
             {'name': 'Bob', 'avenue': 5, 'street': 8}, {'name': 'Edgar', 'avenue': 6, 'street': 13},
             {'name': 'Steven', 'avenue': 3, 'street': 6}, {'name': 'Natalie', 'avenue': 5, 'street': 4}]
```

> Press shift + enter to run the code in the gray boxes.


```python
neighbors
```


```python
# __SOLUTION__ 
neighbors
```




    [{'name': 'Fred', 'avenue': 4, 'street': 8},
     {'name': 'Suzie', 'avenue': 1, 'street': 11},
     {'name': 'Bob', 'avenue': 5, 'street': 8},
     {'name': 'Edgar', 'avenue': 6, 'street': 13},
     {'name': 'Steven', 'avenue': 3, 'street': 6},
     {'name': 'Natalie', 'avenue': 5, 'street': 4}]




```python
fred = neighbors[0]
natalie = neighbors[5]
```


```python
# __SOLUTION__ 
fred = neighbors[0]
natalie = neighbors[5]
```

We'll also plot our neighbors, to get a sense of our data.


```python
import plotly

plotly.offline.init_notebook_mode(connected=True)
trace0 = dict(x=list(map(lambda neighbor: neighbor['avenue'],neighbors)), 
              y=list(map(lambda neighbor: neighbor['street'],neighbors)),
              text=list(map(lambda neighbor: neighbor['name'],neighbors)),
              mode='markers')
plotly.offline.iplot(dict(data=[trace0], layout={'xaxis': {'dtick': 1}, 'yaxis': {'dtick': 1}}))
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>



<div id="4347b30f-6596-468a-9ff9-13153a204476" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("4347b30f-6596-468a-9ff9-13153a204476", [{"mode": "markers", "text": ["Fred", "Suzie", "Bob", "Edgar", "Steven", "Natalie"], "x": [4, 1, 5, 6, 3, 5], "y": [8, 11, 8, 13, 6, 4], "type": "scatter", "uid": "2855ec06-c5ca-11e9-a3f5-3af9d3ad3e0b"}], {"xaxis": {"dtick": 1}, "yaxis": {"dtick": 1}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>



```python
# __SOLUTION__ 
import plotly

plotly.offline.init_notebook_mode(connected=True)
trace0 = dict(x=list(map(lambda neighbor: neighbor['avenue'],neighbors)), 
              y=list(map(lambda neighbor: neighbor['street'],neighbors)),
              text=list(map(lambda neighbor: neighbor['name'],neighbors)),
              mode='markers')
plotly.offline.iplot(dict(data=[trace0], layout={'xaxis': {'dtick': 1}, 'yaxis': {'dtick': 1}}))
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>



<div id="ce7f79cd-2d07-439f-935a-1af71c16e68a" style="height: 525px; width: 100%;" class="plotly-graph-div"></div><script type="text/javascript">require(["plotly"], function(Plotly) { window.PLOTLYENV=window.PLOTLYENV || {};window.PLOTLYENV.BASE_URL="https://plot.ly";Plotly.newPlot("ce7f79cd-2d07-439f-935a-1af71c16e68a", [{"mode": "markers", "text": ["Fred", "Suzie", "Bob", "Edgar", "Steven", "Natalie"], "x": [4, 1, 5, 6, 3, 5], "y": [8, 11, 8, 13, 6, 4], "type": "scatter", "uid": "da4e3978-c5c9-11e9-a505-3af9d3ad3e0b"}], {"xaxis": {"dtick": 1}, "yaxis": {"dtick": 1}}, {"showLink": true, "linkText": "Export to plot.ly"})});</script>


We'll start by focusing on the neighbors Fred and Natalie, and points (4, 8) and (5, 4) respectively.

### Calculating the sides of the triangle

Remember that to calculate the distance, we draw a diagonal line between the two points, form a right triangle around the diagonal line, and then use the Pythagorean Theorem to calculate the hypotenuse of the triangle, that is the distance.  Let's start with imagining we formed a right triangle around the two points and now can move onto calculating the legs of our right triangle. 

Write a function called `street_distance` that calculates how far **in streets** two neighbors are from each other.  So for example, with Natalie at street 4, and Fred at street 8, our `street_distance` function should return the number 4.


```python
def street_distance(first_neighbor, second_neighbor):
    pass
```


```python
# __SOLUTION__ 
def street_distance(first_neighbor, second_neighbor):
        return first_neighbor['street'] - second_neighbor['street']
```

Now execute the code below. As you can see from the comment to the right, the expected returned street distance is $4$.


```python
street_distance(fred, natalie) # 4
```


```python
# __SOLUTION__ 
street_distance(fred, natalie) # 4
```




    4



Write a function called `avenue_distance` that calculates how far in avenues two neighbors are from each other.  The distance should always be positive.


```python
def avenue_distance(first_neighbor, second_neighbor):
    pass
```


```python
# __SOLUTION__ 
def avenue_distance(first_neighbor, second_neighbor):
    return abs(first_neighbor['avenue'] - second_neighbor['avenue'])
```


```python
avenue_distance(fred, natalie) #  1
```


```python
# __SOLUTION__ 
avenue_distance(fred, natalie) #  1
```




    1



### Calculating the distance

Now let's begin writing functions involved with calculating that hypotenuse of our right triangle.  Using the Pythagorean Theorem, $a^2 + b^2 = c^2 $, write a function called `distance_between_neighbors_squared` that calculates $c^2$, the length of the hypotenuse squared.


```python
def distance_between_neighbors_squared(first_neighbor, second_neighbor):
    pass
```


```python
# __SOLUTION__ 
def distance_between_neighbors_squared(first_neighbor, second_neighbor):
    return street_distance(first_neighbor, second_neighbor)**2 + avenue_distance(first_neighbor, second_neighbor)**2
```


```python
distance_between_neighbors_squared(fred, natalie) # 17
```


```python
# __SOLUTION__ 
distance_between_neighbors_squared(fred, natalie) # 17
```




    17



Now let's move onto the next step and write a function called `distance`, that given two neighbors returns the distance between them.  

> You may have to Google some math to do this.


```python
import math
def distance(first_neighbor, second_neighbor):
    pass
```


```python
# __SOLUTION__ 
import math
def distance(first_neighbor, second_neighbor):
    return math.sqrt(distance_between_neighbors_squared(first_neighbor, second_neighbor))
```


```python
distance(fred, natalie) # 4.123105625617661
```


```python
# __SOLUTION__ 
distance(fred, natalie) # 4.123105625617661
```




    4.123105625617661



### Writing Our "Nearest Neighbors" Functions

This next section will work up to building a `nearest_neighbor` function.  This is a function that given one neighbor, will tell us which neighbors are closest.  How do we write something like this? Can we use our calculation of distance between two neighbors to figure out the closest neighbors to an individual?

Sure, we first need to calculate the distances between one neighbor and then all of the others.  Next, we sort those neighbors by their distance from the selected_neighbor.  Finally, we select a given number of the closest neighbors.  Let's work through it.   

Note that we already have a function that calculates the distance between two neighbors.  We may think we could simply use this function to loop through our neighbors, but that would just return a list of distances.  


```python
distances = []
for neighbor in neighbors:
    distance_between = distance(fred, neighbor)
    distances.append(distance_between)

distances
```


```python
# __SOLUTION__ 
distances = []
for neighbor in neighbors:
    distance_between = distance(fred, neighbor)
    distances.append(distance_between)

distances
```




    [0.0,
     4.242640687119285,
     1.0,
     5.385164807134504,
     2.23606797749979,
     4.123105625617661]



The returned list from the above procedure isn't super helpful.  We need to know the person associated with each distance.  

So let's accomplish this by writing a function called `distance_with_neighbor` that works like our distance function but instead of returning a float, returns a dictionary representing the `second_neighbor`, and also adds in the a key value pair indicating distance from the `first_neighbor`.


```python
import math
def distance_with_neighbor(first_neighbor, second_neighbor):
    pass
```


```python
# __SOLUTION__ 
import math
def distance_with_neighbor(first_neighbor, second_neighbor):
    neighbor_with_distance = second_neighbor.copy()
    distance = math.sqrt(distance_between_neighbors_squared(first_neighbor, second_neighbor))
    neighbor_with_distance['distance'] = distance
    return neighbor_with_distance
```


```python
distance_with_neighbor(fred, natalie)
# {'avenue': 5, 'distance': 4.123105625617661, 'name': 'Natalie', 'street': 4}
```


```python
# __SOLUTION__ 
distance_with_neighbor(fred, natalie)
# {'avenue': 5, 'distance': 4.123105625617661, 'name': 'Natalie', 'street': 4}
```




    {'name': 'Natalie', 'avenue': 5, 'street': 4, 'distance': 4.123105625617661}



Now write a function called `distance_all` that returns a list representing the distances between a `first_neighbor` and the rest of the neighbors.  The list should not return the `first_neighbor` in its collection of neighbors. 


```python
def distance_all(first_neighbor, neighbors):
    pass
```


```python
# __SOLUTION__ 
def distance_all(first_neighbor, neighbors):
    remaining_neighbors = list(filter(lambda neighbor: neighbor != first_neighbor, neighbors))
    return list(map(lambda neighbor: distance_with_neighbor(first_neighbor, neighbor), remaining_neighbors))
```


```python
distance_all(fred, neighbors)

# [{'avenue': 1, 'distance': 4.242640687119285, 'name': 'Suzie', 'street': 11},
#  {'avenue': 5, 'distance': 1.0, 'name': 'Bob', 'street': 8},
#  {'avenue': 6, 'distance': 5.385164807134504, 'name': 'Edgar', 'street': 13},
#  {'avenue': 3, 'distance': 2.23606797749979, 'name': 'Steven', 'street': 6},
#  {'avenue': 5, 'distance': 4.123105625617661, 'name': 'Natalie', 'street': 4}]
```


```python
# __SOLUTION__ 
distance_all(fred, neighbors)

# [{'avenue': 1, 'distance': 4.242640687119285, 'name': 'Suzie', 'street': 11},
#  {'avenue': 5, 'distance': 1.0, 'name': 'Bob', 'street': 8},
#  {'avenue': 6, 'distance': 5.385164807134504, 'name': 'Edgar', 'street': 13},
#  {'avenue': 3, 'distance': 2.23606797749979, 'name': 'Steven', 'street': 6},
#  {'avenue': 5, 'distance': 4.123105625617661, 'name': 'Natalie', 'street': 4}]
```




    [{'name': 'Suzie', 'avenue': 1, 'street': 11, 'distance': 4.242640687119285},
     {'name': 'Bob', 'avenue': 5, 'street': 8, 'distance': 1.0},
     {'name': 'Edgar', 'avenue': 6, 'street': 13, 'distance': 5.385164807134504},
     {'name': 'Steven', 'avenue': 3, 'street': 6, 'distance': 2.23606797749979},
     {'name': 'Natalie', 'avenue': 5, 'street': 4, 'distance': 4.123105625617661}]



Finally, write a function called `nearest_neighbors` that given a neighbor, returns a list of neighbors, ordered from closest to furthest from the neighbor.  The function should take an optional third argument that specifies how many "nearest" neighbors are returned.


```python
def nearest_neighbors(first_neighbor, neighbors, number = None):
    pass
```


```python
# __SOLUTION__ 
def nearest_neighbors(first_neighbor, neighbors, number = None):
    number = number or len(neighbors) - 1
    neighbor_distances = distance_all(first_neighbor, neighbors)
    sorted_neighbors = sorted(neighbor_distances, key=lambda neighbor: neighbor['distance'])
    return sorted_neighbors[:number]
```


```python
nearest_neighbors(fred, neighbors, 2)
# [{'avenue': 5, 'distance': 1.0, 'name': 'Bob', 'street': 8},
#  {'avenue': 3, 'distance': 2.23606797749979, 'name': 'Steven', 'street': 6}]
```


```python
# __SOLUTION__ 
nearest_neighbors(fred, neighbors, 2)
# [{'avenue': 5, 'distance': 1.0, 'name': 'Bob', 'street': 8},
#  {'avenue': 3, 'distance': 2.23606797749979, 'name': 'Steven', 'street': 6}]
```




    [{'name': 'Bob', 'avenue': 5, 'street': 8, 'distance': 1.0},
     {'name': 'Steven', 'avenue': 3, 'street': 6, 'distance': 2.23606797749979}]



### Summary

In this lab, you built out the nearest neighbors.  We'll review building out these functions in the next section.
