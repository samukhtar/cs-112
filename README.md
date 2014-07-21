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

"""The blankBoard function takes as arguments, or already knows the value of, a character, boardWidth and a boardHeight. It creates a board of the specified size, as a two dimensional list, and fills it with the character specified. For example, if you called the function as blankBoard('X',3,2), your function would return [['X', 'X', 'X'], ['X', 'X', 'X']]. If you called it with blankBoard('1',1,2), it would return [['1'], ['1']].
The populateBoard function takes as arguments, or already knows the value of, a mineList, boardWidth and a boardHeight. It creates a board of the specified size, as a two dimensional list, and fills it with the proper values.

The board will be a two dimensional list that will contain an X character in every position specified by the incoming mineList. All other tiles in the board will be set to the character 0, unless they neighbor a tile with a mine in it. If they do, you will increment the 0 by the number of neighboring mines to that tile, and store that value. For example, if you called the function as populateBoard([1,5],3,4), your function would return [['1', 'X', '2'], ['1', '2', 'X'], ['0', '1', '1'], ['0', '0', '0']].

Note that you will have to design your own algorithm for this function - as in many software specifications, we are only supplying you with the input and output specifications - the rest is up to you. As a hint, you should use all of the functions you wrote so far (blankBoard, getNeighborLabels, verifyNeighbor); use the eval( ) function to convert the strings these functions returned into lists or boolean values as needed. Therefore, you must move your project2.py file into the same directory as the current project, if it is not there already. The template has taken care of pointing your new code to the project2.py file. """

#project 3
def blankBoard(character,boardWidth,boardHeight):
	board = []
	ctr=0
	while ctr < boardHeight:
		board.append([])
		ctr+=1
	for i in board:
		ctr2=0
		while ctr2<boardWidth:
			i.append(str(character))
			ctr2+=1
	
	#YOUR CODE GOES HERE
	#remember to indent all code inside this function
	
	return board

#project 3
def populateBoard (mineList, boardWidth, boardHeight):
	board = []
	ctr=0
	me=0
	while ctr < boardHeight:
		board.append([])
		ctr+=1
	for i in board:
		ctr2=0
		while ctr2<boardWidth:
			ctr3=0
			for j in mineList:
				x = verifyNeighbor(boardWidth, boardHeight, j, me)
				if x == True:
					ctr3+=1
			if me not in mineList:
				i.append(str(ctr3))
			else:
				i.append('X')
			ctr2+=1
			me+=1
	return board


"""The displayBoard function takes as arguments, or already knows the value of, a board and a boardWidth. It returns a string representation of the board passed in, which is a two dimensional list.

The function will return the contents of the board in the following format:
It will have a header that starts with the < character, followed by some number of dashes that will depend on the width of the board, followed by a > sign, and then a newline. The total number of dashes is equal to two times the width plus one, except if the board is of width 1 (we specify the latter below).
After the header, each row of the board is printed. A row starts with a < character, followed by a space, followed by the contents of the row (each will be one character long), separated by a single space, followed by a space and a closing >, and then a newline.
Finally, there will be a footer which is identical to the header.

For example, a call to the function with displayBoard([['0','0']],2) will return the string 
<----->\n< 0 0 >\n<----->

If the width of the board is 1, such as displayBoard([['0']],1) will return the string
<----->\n< 0 >\n<----->

When you code this function, make sure to add a newline to the result you will return, otherwise it will not pass the test cases. You don't need the newlines at the end of your test cases.
The collectEmpty function takes as arguments, or already knows the value of, a board, boardWidth, boardHeight, and a move to be made. It uses the move and determines which of its neighbors are empty (i.e. they store the character 0). Of all those neighbors, it keeps repeating this search until there are no more adjacent empty neighbors. Note that we are only looking for adjacent neighbors here, defined for this function as either directly above, below, right, or left of the desired tile (i.e. they must share an edge). This function will not return all empty tiles in the board, but instead is meant to illustrate all the empty tiles returned by clicking the lowest-right tile in the last image above, for example. If the move tile is empty, it also returns that, in addition to the other empty tiles.

The board will be a two dimensional list that will contain either an integer, or the # or X characters. The numbers on the board don't have to make sense in terms of mine placement. Your code will return all tiles with a 0 that are adjacent to the move as described above. For example, if you called the function as collectEmpty([['1','X','2'], ['1','2','X'], ['0','1','1'], ['0','0','0']],3,4,9), your function would return [6, 9, 10, 11]. The list that you return should be sorted in the natural ascending order.

To make things easier, I have modified the getNeighborLabels function from project 2 to have another version that takes a third boolean argument, that will decide whether to return all neighbors (as we did in project 2), or only the neighbors that share an edge (which we will find useful for this function).

This function seems trivial, but it is not. Do not wait until the last minute to start coding. In order to correctly calculate all empty, adjacent neighbors of a tile, you will probably want to keep track of neighbors and tiles that you are comparing by pairing them in lists and storing these lists-of-two in a list for processing.

Note that you will have to design your own algorithm for this function - as in many software specifications, we are only supplying you with the input and output specifications - the rest is up to you. As a hint, you should use the functions you wrote so far (getNeighborLabels, verifyNeighbor)."""

def modifiedGetNeighborLabels(boardWidth,boardHeight,me):
	lis=[]
	if me-boardWidth >= 0:
		lis.append(me-boardWidth)
	if me+boardWidth < boardHeight*boardWidth:
		lis.append(me+boardWidth)
	if me%boardWidth != 0:
		lis.append(me-1)
	if me%boardWidth != boardWidth-1:
		lis.append(me+1)
	return lis
def collectEmpty(boardKey,boardWidth,boardHeight,move):
	empties=[]
	dict={}
	ctr = 0
	y=[]
	for i in boardKey:
		for j in i:
			dict[ctr]=j
			ctr+=1
	x=modifiedGetNeighborLabels(boardWidth,boardHeight,move)
	for i in x:
		if dict[i]=='0' and i not in empties:
			empties.append(i)
			y=modifiedGetNeighborLabels(boardWidth,boardHeight,i)
		for j in y:
			if dict[j]=='0' and j not in empties:
				x.append(j)
	return sorted(list(set(empties)))
	
	#YOUR CODE GOES HERE
	#remember to indent all code inside this function
