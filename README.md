giftSuggestor
=============

Gift Suggestor is an online tool for suggesting various combinations products. It acts as an assistance tool for customers who are looking for the right combination of gifts for a cost of specific amount. It has a simple interface for the customers to enter there inputs.

Inputs:
Online tool has two options for the customers. 
  1) Customer can enter the maximum amount for which they wish to gift.
  2) Number of products they wish to gift.
  
Output:
Once the customer inputs his choices, a table containning first 10 combinations of the products will be displayed. 
Now if the customer is not satisfied with the options provided to him, he can press "next" button. Once again a table containing 10 more suggestions will be presented. 
Customer has an option of changing his inputs anytime. If the customer has entered a request for n products with s amount and after few suggestions he wants it to be changed. Then he can enter new values for maximum amount and number of gifts.

Execution:

The data required for the tool is accessed from the database of Zappos. For fetching the data, developer API's provided by the platform of Zappos are used. 

API's used:

Brand API : This API is used to fetch all the brands sold by Zappos.
Search API : Now we will search all the products of a particular brand. Here the API returns a lot of data about each product. Only the relevant required is stored. The Price, ProductID and the image associated with each product are stored.

Algorithm:
The products are sorted in the ascending order of their price. The next step is the subset generation procedure. All the combinations of products whose ceil(sums) will be equal to the maximum_sum will be generated.
We start iterating through the sorted array. The problem of subset creation has a exponential time complexity. WE will be facing products if we try to iterate through the entire array(number of product retrieved can go to upwards of 10000) for each subset creation .

Steps taken to decrease the search space :
  1) The products whose price is greater than 'maximum_price', will not be considered.
  2) Deletion of few products with price less than maximum_price
    Eg: Customer wants suggestions for 3 products with maximum price 15. Consider a minimum price of any product in Zappos store     is 3. Then there is no point in having products of price between 12 and 15. So these products also will not be considered       for search.
  3) Dynamically deciding the search space.
    Consider customer wants suggestion for 3 products with maximum price 20. Now at some stage in search space we have selected     two products with price 3 and 4. Then we can consider only the products with price greater than 20-(3+4). So all     the remaining with price less than 13, will be discarded for this search.
  4) Once the program calculates 10 sets of products, we will display the products on to the screen. This is done because there      is no point in calculating all the combinations, if the customer selects from the first page itself. But if the customer is     not satisfied with first 10 suggestions, 'next' button can be pressed. Now next 10 suggestions will be displayed.
  
  Once all the product suggestions, customer can enter new values for maximum_price and maximum_amount.
  
