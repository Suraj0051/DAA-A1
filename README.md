# DAA-A1

This project is an implimentation of the following research paper

Fernández, J., Cánovas, L., & Pelegrın, B. (2000). Algorithms for the decomposition of a polygon into ́
convex polygons. European Journal of Operational Research, 121(2), 330-342.
https://doi.org/10.1016/S0377-2217(99)00033-8
To run the code first run generate_points.py file with the following prompt
python generate_points.py 15 #here 15 represend the total number of vertices or nodes of the polygon.
this will create an input.txt file with the following content For Ex:

15
303 303
305 384
363 543
249 624
157 919
410 700
156 981
508 946
679 767
901 989
832 809
772 352
827 219
748 309
613 17
Followed by run

g++ Decompose.cpp 
./a.out
This will generate output.txt containing Ex:

303 303
305 384
363 543

363 543
249 624
157 919
410 700

410 700
156 981
508 946
679 767

679 767
901 989
832 809

679 767
832 809
772 352

772 352
827 219
748 309

748 309
613 17
303 303
363 543
410 700
679 767

748 309
679 767
772 352
Decomposed polygons.

To visualize these decomposition run

python Visualize decomposed polygon.py
The provided code is an implementation of a polygon partitioning algorithm based on the concept of decomposing a given non-convex polygon into smaller convex polygons. The algorithm utilizes the Doubly Connected Edge List (DCEL) data structure to represent the polygon and perform the decomposition.

Here is a step-by-step explanation of the algorithm:

The code begins with the definition of various data structures such as Point, HalfEdge, Face, and DCEL. These structures are used to store the vertices, edges, and faces of the polygon.

The decompose function is responsible for creating the initial DCEL representation of the polygon. It takes a set of vertices as input and constructs the edges and faces of the polygon based on the vertices' order.

The angle function determines whether the interior angle at a given point is less than 180 degrees. It calculates the cross product of two vectors formed by three points and checks the sign of the cross product to determine the angle's orientation.

The notch function determines if a given point is a "notch" or not. A notch is defined as a point in the polygon that has an interior angle greater than 180 degrees. It calls the angle function to check if the angle at the given point is less than 180 degrees. If not, it considers the point as a notch.

The next function returns the point that follows a given point in clockwise order based on the vertices' order.

The side function is used to determine whether a given point is on the left side, right side, or on the line segment formed by two other points. It calculates the cross product between vectors formed by the three points and checks the sign of the result to determine the relative position.

The rectangle function is responsible for finding the smallest possible rectangle (parallel to the axes) that encloses a given convex polygon. It iterates over the vertices of the polygon to find the minimum and maximum x and y coordinates, which define the rectangle.

The remove_duplicates function removes any duplicate vertices from a given list of points. It iterates over the list and removes any points that have the same coordinates as previously encountered points.

The check_if_same function compares the vertices of the current convex polygon with the original vertices. If they are not the same, it updates the vertices of the convex polygon to match the original vertices. This is necessary to handle the case where the convex polygon becomes the same as the original polygon due to the decomposition process.

The main Decompose_polygon function implements the polygon partitioning algorithm. It takes the original set of vertices as input and returns a list of decomposed convex polygons.

The function starts by initializing variables and data structures. It adds the first vertex of the polygon to the convex_polygon list.

The algorithm iterates until the number of vertices in the vertice list is reduced to 3 or less. This is because a polygon with 3 or fewer vertices is already convex and does not need further decomposition.

Inside the iteration, the algorithm checks if the current convex_polygon is the same as the original polygon. If so, it adds the convex_polygon to the result list and returns the result.

If the convex_polygon has only 2 points, it updates the p1 and p2 variables accordingly, clears the convex_polygon list, and removes the first vertex from the vertice list. This step handles the case where the convex polygon has reduced to a line segment.

If the convex_polygon has

more than 2 points, the algorithm finds the next vertex (p3) in the vertice list based on the current vertex (p2) and the previous vertex (p1). It checks if p3 is a notch using the notch function.

If p3 is a notch, the algorithm proceeds to check if the notch lies outside the smallest possible enclosing rectangle of the current convex_polygon. If it does, the notch is discarded, and the algorithm moves on to the next vertex (p2 becomes p3). Otherwise, the notch is considered as a valid point for further decomposition.

If p3 is not a notch, the algorithm checks if it lies on the correct side of the current convex_polygon using the side function. If it does, p3 is added to the convex_polygon, and the algorithm moves on to the next vertex (p1 becomes p2, p2 becomes p3).

After the iteration is complete, the algorithm adds the remaining convex_polygon to the result list.

Finally, the Decompose_polygon function returns the result list containing the decomposed convex polygons.

In summary, the algorithm works by iteratively adding vertices to a convex polygon until certain conditions are met. It handles notches by discarding those outside the smallest enclosing rectangle and selecting those on the correct side of the convex polygon. The process continues until the polygon is fully decomposed, and the resulting convex polygons are stored in the result list.
