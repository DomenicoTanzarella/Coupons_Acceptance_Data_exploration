
# Will a Customer Accept the Coupon?

## Introduction and Context 

Imagine driving through town and a coupon is delivered to your cell phone for a restaraunt near where you are driving. Would you accept that coupon and take a short detour to the restaraunt? Would you accept the coupon but use it on a sunbsequent trip? Would you ignore the coupon entirely? What if the coupon was for a bar instead of a restaraunt? What about a coffee house? Would you accept a bar coupon with a minor passenger in the car? What about if it was just you and your partner in the car? Would weather impact the rate of acceptance? What about the time of day?

[This notebook](https://github.com/DomenicoTanzarella/Coupons_Acceptance_Data_exploration/blob/main/Coupon_acceptance.ipynb) will try to answer to such questions by analyzing a dataset related coupon acceptance

# Data Understanding

##   Data description

The attributes of this data set include:

1.  User attributes
    -   Gender: male, female
    -   Age: below 21, 21 to 25, 26 to 30, etc.
    -   Marital Status: single, married partner, unmarried partner, or widowed
    -   Number of children: 0, 1, or more than 1
    -   Education: high school, bachelors degree, associates degree, or graduate degree
    -   Occupation: architecture & engineering, business & financial, etc.
    -   Annual income: less than \$12500, \$12500 - \$24999, \$25000 - \$37499, etc.
    -   Number of times that he/she goes to a bar: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -   Number of times that he/she buys takeaway food: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -   Number of times that he/she goes to a coffee house: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -   Number of times that he/she eats at a restaurant with average expense less than \$20 per person: 0, less than 1, 1 to 3, 4 to 8 or greater than 8
    -   Number of times that he/she goes to a bar: 0, less than 1, 1 to 3, 4 to 8 or greater than 8

2.  Contextual attributes
    -   Driving destination: home, work, or no urgent destination
    -   Location of user, coupon and destination: we provide a map to show the geographical location of the user, destination, and the venue, and we mark the distance between each two places with time of driving. The user can see whether the venue is in the same direction as the destination.
    -   Weather: sunny, rainy, or snowy
    -   Temperature: 30F, 55F, or 80F
    -   Time: 10AM, 2PM, or 6PM
    -   Passenger: alone, partner, kid(s), or friend(s)

3.  Coupon attributes
    -   time before it expires: 2 hours or one day
    
##  Early data exploration report

The dataset has 12684 entries with 26 Data columns:
    
 0   destination              12684 non-null  object
 
 1   passanger                12684 non-null  object
 
 2   weather                   12684 non-null  object
 
 3   temperature            12684 non-null  int64 
 
 4   time                         12684 non-null  object
 
 5   coupon                    12684 non-null  object
 
 6   expiration               12684 non-null  object
 
 7   gender                    12684 non-null  object
 
 8   age                          12684 non-null  object
 
 9   maritalStatus         12684 non-null  object
 
 10  has_children         12684 non-null  int64 
 
 11  education             12684 non-null  object
 
 12  occupation           12684 non-null  object
 
 13  income                 12684 non-null  object
 
 14  car                            108 non-null    object
 
 15  Bar                       12577 non-null  object
 
 16  CoffeeHouse       12467 non-null  object
 
 17  CarryAway          12533 non-null  object
 
 18  RestaurantLessThan20  12554 non-null  object
 
 19  Restaurant20To50         12495 non-null  object
 
 20  toCoupon_GEQ5min     12684 non-null  int64 
 
 21  toCoupon_GEQ15min    12684 non-null  int64 
 
 22  toCoupon_GEQ25min    12684 non-null  int64 

 23  direction_same        12684 non-null  int64 
 
 24  direction_opp         12684 non-null  int64 
 
 25  Y                               12684 non-null  int64

We have only two data types that are are 'object' and 'int64'.
  

## look for MISSING DATA

We have six data columns with missing data:

car                                        12576

Bar                                          107

CoffeeHouse                                  217

CarryAway                                    151

RestaurantLessThan20                         130

Restaurant20To50                             189

# Data Preparation and cleansing

First, will rename Column 'Y' in 'Coupon Accepted' so to make the dataset more clear.

**time**,  **age**  and  **income** data are identified as objects but really should be int64, with time expressed in hours and income entry replaced with its average.

Also,  **RestaurantLessThan20**  and  **Restaurant20To50**  ,  **carryaway**  need to be numeric so we will need to average them

For missing data, we can definitely drop  **car**  column. 
Also, I  replace NaN values for  **CoffeeHouse**,  **CarryAway**,  **RestaurantLessThan20**  and  **Restaurant20To50**  either with average values or the most probable ones (depending on the percentage missing)

# Data Exploation

- We will start figuring out the proportion of couponse accepted by type of coupon

- Then we will analyze Bar Coupons finding the following:

The acceptance rate of people going to a bar depends on how many times they go to the bar in a month. The more they go, the highest is the acceptance rate. 

-We analyze also the coffe house coupons, finding that people with higher probability of accepting coupons are:
   -   young customers
   -   frequent customers
   -   non widowed
   
and, as common sense could suggest, when the temperature is hot (80+ degrees) is more likely that coupons are accepted compared to other less hot days (people will go to the coffee house for A/C and cold beverage)

Finally, does not look like there is much correlation of coupon acceptance with income or gender
