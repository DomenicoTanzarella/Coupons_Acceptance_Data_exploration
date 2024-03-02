
# Will a Customer Accept the Coupon?

## Introduction and Context 

Imagine driving through town and a coupon is delivered to your cell phone for a restaraunt near where you are driving. Would you accept that coupon and take a short detour to the restaraunt? Would you accept the coupon but use it on a subsequent trip? Would you ignore the coupon entirely? What if the coupon was for a bar instead of a restaraunt? What about a coffee house? Would you accept a bar coupon with a minor passenger in the car? What about if it was just you and your partner in the car? Would weather impact the rate of acceptance? What about the time of day?

[This notebook](https://github.com/DomenicoTanzarella/Coupons_Acceptance_Data_exploration/blob/main/Coupon_acceptance.ipynb) will try to answer to such questions by analyzing a coupon's acceptance related dataset

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
    
 -   destination       with       12684 non-null  object
 
 -   passanger        with        12684 non-null  object
 
 -   weather         with          12684 non-null  object
 
 -   temperature    with        12684 non-null  int64 
 
 -   time           with         12684 non-null  object
 
 -   coupon         with        12684 non-null  object
 
 -   expiration    with           12684 non-null  object
 
 -   gender        with            12684 non-null  object
 
 -   age          with                12684 non-null  object
 
 -   maritalStatus    with     12684 non-null  object
 
 -  has_children    with     12684 non-null  int64 
 
 -  education      with       12684 non-null  object
 
 -  occupation    with       12684 non-null  object
 
 -  income        with         12684 non-null  object
 
 -  car          with                  108 non-null    object
 
 -  Bar         with              12577 non-null  object
 
 -  CoffeeHouse     with  12467 non-null  object
 
 -  CarryAway      with    12533 non-null  object
 
 -  RestaurantLessThan20 with 12554 non-null  object
 
 -  Restaurant20To50   with      12495 non-null  object
 
 -  toCoupon_GEQ5min  with   12684 non-null  int64 
 
 -  toCoupon_GEQ15min  with  12684 non-null  int64 
 
 -  toCoupon_GEQ25min  with  12684 non-null  int64 

 -  direction_same   with     12684 non-null  int64 
 
 -  direction_opp    with     12684 non-null  int64 
 
 -  Y                    with           12684 non-null  int64

We have only two data types that are are 'object' and 'int64'.
  

## MISSING DATA

We have six data columns with missing data:

- car:                                        12576

- Bar:                                          107

- CoffeeHouse:                                  217

- CarryAway:                                    151

- RestaurantLessThan20:                         130

- Restaurant20To50:                             189

# Data Preparation and cleansing

First, will rename Column 'Y' in 'Coupon Accepted' so to make the dataset more clear.

**time**,  **age**  and  **income** data are identified as objects but really should be int64, with time expressed in hours and income entry replaced with its average.

Also,  **RestaurantLessThan20**  and  **Restaurant20To50**  ,  **carryaway**  need to be numeric so we will need to average them

For missing data, we can definitely drop  **car**  column. 
Also, I  replace NaN values for  **CoffeeHouse**,  **CarryAway**,  **RestaurantLessThan20**  and  **Restaurant20To50**  either with average values or the most probable ones (depending on the percentage missing)

# Data Exploration

- We will start figuring out the proportion of coupons accepted by type of coupon

- Then we will analyze Bar Coupons finding the following:

The acceptance rate of people going to a bar depends on how many times they go to the bar in a month: the more they go, the highest is the acceptance rate. 

We analyze also the coffee house coupons, finding that people with higher coupons acceptance rate are:
   -   young customers
   -   frequent customers
   -   non widowed
   
and, as common sense could suggest, when the temperature is hot (80+ degrees) is more likely that coupons are accepted compared to other less hot days (people will go to the coffee house for A/C and cold beverage)

Finally, does not look like there is much correlation of coupon acceptance with income or gender
