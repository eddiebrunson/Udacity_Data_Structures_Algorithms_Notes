# Lesson 3: How to Solve Problems 


--> Days between Dates problem 

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
5. First Step 

Quiz:

What is the first thing we should do to solve a problem like this one?

* Start writing code
* Make sure we understand the problem 
* Search Google for the answer 
* Work out an algorithm that solves it

--> The problem is defined by possible inputs 

Understanding a Computational Problem

First Rule to solving problems

0. Don't panic
1. Figure out the inputs
2. What are the outputs?
3. Solve the problem!
4. Simple mechanical solution
5. Develop solution incrementally and test as you go


Given your birthday and the current date, calculate your age in days.

Inputs: two dates

9. How are inputs are represented? 


* second date must not be before the first date -> Defensive Programming 
* Gregorian Calendar ( 15 Oct 1582)

How are inputs represented?
def daysBetweenDates( year1, month1, day1, year2, month2, day2):
--> there are other ways to package the year, month and days

10. What are the outputs?

Return a number giving the number of days between the first date and the second date

___

**Problem statement**

Define a procedure, daysBetweenDates, that takes two dates as inputs and returns the number of days between the first date and second date. Each date is passed in as three numbers giving a valid year, month, and day in the Gregorian calendar. The second date must not be before the first. 

--> Next step is to work out examples! 

Best Strategy

A stub is a dummy implementation of the method. It can be used for testing before you code the whole function.

In order to answer this question, you should think about the dependencies between the various steps, but also about what order of implementing and testing them will most likely to efficiently lead to a correct solution. It's definitely a subjective question, and there are many reasonable answers to this question. 

1. write stub daysInMonth(year, month) that always returns 30
2. modify nextDay(year, month, day) to use daysInMonth(year, month)
3. test nextDay(year, month, day) using stub daysInMonth
4. modify daysInMonth(year, month) to be correct except for leap years 
5. then repeat step 3 to test again
6. write isLeapYear(year)
7. test isLeapYear(year)
8. modify daysInMonth(year, month) to account for leap years
9. test daysBetweenDates(...) for all test cases
10.
11.

___

**Finish daysBetweenDates**

```Python
# Credit goes to Websten from forums
#
# Use Dave's suggestions to finish your daysBetweenDates
# procedure. It will need to take into account leap years
# in addition to the correct number of days in each month.

def nextDay(year, month, day):
    """Simple version: assume every month has 30 days"""
    if day < 30:
        return year, month, day + 1
    else:
        if month == 12:
            return year + 1, 1, 1
        else:
            return year, month + 1, 1
        
def dateIsBefore(year1, month1, day1, year2, month2, day2):
    """Returns True if year1-month1-day1 is before year2-month2-day2. Otherwise, returns False."""
    if year1 < year2:
        return True
    if year1 == year2:
        if month1 < month2:
            return True
        if month1 == month2:
            return day1 < day2
    return False        

def daysBetweenDates(year1, month1, day1, year2, month2, day2):
    """Returns the number of days between year1/month1/day1
       and year2/month2/day2. Assumes inputs are valid dates
       in Gregorian calendar."""
    # program defensively! Add an assertion if the input is not valid!
    assert not dateIsBefore(year2, month2, day2, year1, month1, day1)
    days = 0
    while dateIsBefore(year1, month1, day1, year2, month2, day2):
        year1, month1, day1 = nextDay(year1, month1, day1)
        days += 1
    return days

def test():
    test_cases = [((2012,1,1,2012,2,28), 58), 
                  ((2012,1,1,2012,3,1), 60),
                  ((2011,6,30,2012,6,30), 366),
                  ((2011,1,1,2012,8,8), 585 ),
                  ((1900,1,1,1999,12,31), 36523)]
    
    for (args, answer) in test_cases:
        result = daysBetweenDates(*args)
        if result != answer:
            print "Test with data:", args, "failed"
        else:
            print "Test case passed!"

test()
```

35. Solution Step 1

```Python
def daysInMonth(year, month): 
	return 30

def nextDay(year, month, day):
    """Simple version: assume every month has 30 days"""
    """Warning: this version incorrrectly assumes all months have 30 days!"""
    if day < daysInMonth(year. ,month):
        return year, month, day + 1
    else:
        if month == 12:
            return year + 1, 1, 1
        else:
            return year, month + 1, 1
        
def dateIsBefore(year1, month1, day1, year2, month2, day2):
    """Returns True if year1-month1-day1 is before year2-month2-day2. Otherwise, returns False."""
    if year1 < year2:
        return True
    if year1 == year2:
        if month1 < month2:
            return True
        if month1 == month2:
            return day1 < day2
    return False        

def daysBetweenDates(year1, month1, day1, year2, month2, day2):
    """Returns the number of days between year1/month1/day1
       and year2/month2/day2. Assumes inputs are valid dates
       in Gregorian calendar."""
    # program defensively! Add an assertion if the input is not valid!
    assert not dateIsBefore(year2, month2, day2, year1, month1, day1)
    days = 0
    while dateIsBefore(year1, month1, day1, year2, month2, day2):
        year1, month1, day1 = nextDay(year1, month1, day1)
        days += 1
    return days

def test():
    test_cases = [((2012,1,1,2012,2,28), 58), 
                  ((2012,1,1,2012,3,1), 60),
                  ((2011,6,30,2012,6,30), 366),
                  ((2011,1,1,2012,8,8), 585 ),
                  ((1900,1,1,1999,12,31), 36523)]
    
    for (args, answer) in test_cases:
        result = daysBetweenDates(*args)
        if result != answer:
            print "Test with data:", args, "failed"
        else:
            print "Test case passed!"

def test():
	# test with 30-day months!
	assert daysBetweenDates(2013, 1, 1, 2013, 1, 1) == 0
	assert daysBetweenDates(2013, 1, 1, 2013, 1, 2) == 1
	assert nextDay(2013, 1, 1) == (2013, 1, 2)
	assert nextDay(2013, 4, 30) == (2013, 5, 1)
	assert nextDay(2012, 12, 31) == (2013, 1, 1)
	print "Tests finished!"

 
test()

```

36. Solution Step II

```Python
def daysInMonth(year, month): 
	if month == 1 or month == 3 or month == 5 or month == 7 \
	    or month == 8 or month == 10 or month == 12: 
	     return 31
	else:
		if month == 2:
			return 28
		else: 
	return 30


def nextDay(year, month, day):
    """Simple version: assume every month has 30 days"""
    """Warning: this version incorrrectly assumes all months have 30 days!"""
    if day < daysInMonth(year. ,month):
        return year, month, day + 1
    else:
        if month == 12:
            return year + 1, 1, 1
        else:
            return year, month + 1, 1
        
def dateIsBefore(year1, month1, day1, year2, month2, day2):
    """Returns True if year1-month1-day1 is before year2-month2-day2. Otherwise, returns False."""
    if year1 < year2:
        return True
    if year1 == year2:
        if month1 < month2:
            return True
        if month1 == month2:
            return day1 < day2
    return False        

def daysBetweenDates(year1, month1, day1, year2, month2, day2):
    """Returns the number of days between year1/month1/day1
       and year2/month2/day2. Assumes inputs are valid dates
       in Gregorian calendar."""
    # program defensively! Add an assertion if the input is not valid!
    assert not dateIsBefore(year2, month2, day2, year1, month1, day1)
    days = 0
    while dateIsBefore(year1, month1, day1, year2, month2, day2):
        year1, month1, day1 = nextDay(year1, month1, day1)
        days += 1
    return days

def test():
    test_cases = [((2012,1,1,2012,2,28), 58), 
                  ((2012,1,1,2012,3,1), 60),
                  ((2011,6,30,2012,6,30), 366),
                  ((2011,1,1,2012,8,8), 585 ),
                  ((1900,1,1,1999,12,31), 36523)]
    
    for (args, answer) in test_cases:
        result = daysBetweenDates(*args)
        if result != answer:
            print "Test with data:", args, "failed"
        else:
            print "Test case passed!"

def test():
	# test with 30-day months!
	assert daysBetweenDates(2013, 1, 1, 2013, 1, 1) == 0
	assert daysBetweenDates(2013, 1, 1, 2013, 1, 2) == 1
	assert nextDay(2013, 1, 1) == (2013, 1, 2)
	assert nextDay(2013, 4, 30) == (2013, 5, 1)
	assert nextDay(2012, 12, 31) == (2013, 1, 1)
	assert nextDay(2013, 2, 28) == (2013, 3, 1)
	assert nextDay(2013, 9, 30) == (2013, 10, 1)
	assert daysBetweenDates(2013, 1, 1, 2014, 1, 1) == 365
	print "Tests finished!"

 
test()

```


