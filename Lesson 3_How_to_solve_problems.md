# Lesson 3: How to Solve Problems 


\--> Days between Dates problem 

Given your birthday and the current date, calculate your agin in days. COmpenstate for leap days. Assume that the birthday and current date are correct dates ( and no time travel). Simply put, if you were born 1 Jan 2012 and todays date is 2 Jane 2012 you are 1 day old. 

Skeleton

```Python

daysOfMonths = [ 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]

def isLeapYear(year):
	##
	# Your code here. Return True or False
	# Pseudo code for this algorithm is found at 
	# http://en.wikipedia.org/wiki/Leap_year#Algorithm
	##

	def daysBetweenDates(y1, m1, d1, y2, m2, d2):
		##
		# Your code here. 
```

Days Between Dates:

```Python
def daysBetweenDates(year1, month1, day1, year2, month2, day2):
    """
    Calculates the number of days between two dates.
    """
    
    # TODO - by the end of this lesson you will have
    #  completed this function. You do not need to complete
    #  it yet though! 
    
    return 0

def testDaysBetweenDates():
    
    # test same day
    assert(daysBetweenDates(2017, 12, 30,
                              2017, 12, 30) == 0)
    # test adjacent days
    assert(daysBetweenDates(2017, 12, 30, 
                              2017, 12, 31) == 1)
    # test new year
    assert(daysBetweenDates(2017, 12, 30, 
                              2018, 1,  1)  == 2)
    # test full year difference
    assert(daysBetweenDates(2012, 6, 29,
                              2013, 6, 29)  == 365)
    
    print("Congratulations! Your daysBetweenDates")
    print("function is working correctly!")
    
testDaysBetweenDates()
```

