cs-112
======
"""The getNeighborLabels function takes as arguments, or already knows the value of, the boardWidth and a current tile called me. You can imagine the user has entered these values, and they are stored in variables called boardWidth and me; you do not need to ask the user to enter these values. In general the tiles of a board are always numbered, starting at zero. For example, on a board with a width of 4 and a height of 3, the tiles would be labeled as:
 0 	 1 	 2 	 3 
 4 	 5 	 6 	 7 
 8 	 9 	10	11

For this function, you will simply be performing the following calculations and storing each value in a string:
me – boardWidth – 1	me – boardWidth	me – boardWidth + 1
me – 1	me	me + 1
me + boardWidth – 1	me + boardWidth	me + boardWidth+ 1

Your function should find all the neighbors of the tile me, and return them as a string with the tiles in sorted order (if you write your algorithm "the easy way," it will be natural for the tiles to be in sorted order). For example, a call to the function with getNeighborLabels(5,0) (here 5 is the boardWidth and 0 is the me argument) would return the string of neighbors "[1, 4, 5, 6]". Each list will start and end with a bracket, and each element of the list will be separated from a previous element by a comma and then a space.

If the board provided is invalid, (i.e. its width is not a natural number), your function should return a string of "invalid board!". You may assume that the me tile will always be an integer, however your method should never return any negative neighbors, as these will be impossible to fit on any board. Note that we don't know if the me tile provided is ever too large, because we do not have the height of the board in this function. You can always assume that the board that would be calling this function provides a valid me tile for this project, and that all arguments are integers. If one of the neighbors has the same value as the me, you should include that in the result. Your result should also NOT have any duplicates - you need to check that you didn't already add a tile like that to the string, before adding it. 
Although your function above will work in cases where the me tile is in the middle of the board, it will calculate incorrect values if the tile is along an edge. Therefore, we are going to write another function to verify the labels returned by the function above.

The second function you will write for this project is called verifyNeighbor. This function takes as arguments a boardWidth, boardHeight, neighbor, and a me tile (you can assume a user already entered these values, and you have access them as stored variables under these names). It will return either the string "True" or "False". For this function, imagine that the tile me is tile 3. Then all of its neighbors would be 2, 6, and 7. A neighbor is any tile on the board that touches (even in a single point) the tile me. A tile has at most eight neighbors. For example, a call to the function with verifyNeighbor(4,3,4,3) would return "False", because although 4 was a neighbor that could have been returned from the getNeighborLabels function, it is NOT a valid neighbor of 3 on this board."""
#project 2
def getNeighborLabels (boardWidth, me):

	#YOUR CODE GOES HERE
	#remember to indent all code inside this function
	if boardWidth <= 0:
		return 'invalid board!'
	lis='['
	a=me-boardWidth-1
	if a>=0:
		lis+=str(a)+', '
	b=me-boardWidth
	if b>=0 and b != a:
		lis+=str(b)+', '
	c=me-boardWidth+1
	if c>=0 and c != a and c != b:
		lis+=str(c)+', '
	d=me-1
	if d>=0 and d != a and d!=b and d!=c:
		lis+=str(d)+', '
	e=me+1
	if e>=0 and e != a and e!=b and e!=c and e!=d:
		lis+=str(e)+', '
	f=me+boardWidth-1
	if f>=0 and f != a and f != b and f != c and f != d and f != e:
		lis+=str(f)+', '
	g=me+boardWidth
	if g>=0 and g != a and g!=b and g!=c and g!=d and g!=e and g!=f:
		lis+=str(g)+', '
	h=me+boardWidth+1
	if h>=0 and h != a and h!=b and h!=c and h!=d and h!=e and h!=f and h!=g:
		lis+=str(h)+']'
	
	result = lis
	
	return result

#project 2	
def verifyNeighbor (boardWidth, boardHeight, neighbor, me):
	
	#YOUR CODE GOES HERE
	if boardWidth <= 0:
		return 'invalid board!'
	row=(me//boardWidth)+1
	column=(me%boardWidth)+1
	if (me-boardWidth-1)>=0 and row!=1 and column!=1:
		a=me-boardWidth-1
	else:
		a=-1000
	if (me-boardWidth)>=0 and row!=1:
		b=me-boardWidth
	else:
		b=-1000
	if (me-boardWidth+1)>=0 and row!=1 and column!=boardWidth:
		c=me-boardWidth+1
	else:
		c=-1000
	if (me-1)>=0 and column!=1:
		d=me-1
	else:
		d=-1000
	if (me+1)>=0 and column!=boardWidth:
		e=me+1
	else:
		e=-1000
	if (me+boardWidth-1)>=0 and row!=boardHeight and column!=1:
		f=me+boardWidth-1
	else:
		f=-1000
	if (me+boardWidth)>=0 and row!=boardHeight:
		g=me+boardWidth
	else:
		g=-1000
	if (me+boardWidth+1)>=0 and row!=boardHeight and column!=boardWidth:
		h=me+boardWidth+1
	else:
		h=-1000
	if neighbor==a or neighbor==b or neighbor==c or neighbor==d or neighbor==e or neighbor==f or neighbor==g or neighbor==h:
		return True
	else:
		return False
	#remember to indent all code inside this function
