# Title: Nitrogen Ice-cream Shop Monte Carlo Simulation
![Nitro ice-cream pic](https://torontocitykey.com/wp-content/uploads/2017/11/Labsense-1.jpg "Nitrogen Ice-cream")

## Team Members:
Yuejun Wu, Thuong Phan

# Monte Carlo Simulation Scenario & Purpose:
### Background
We simulate one day operation of a nitrogen ice-cream shop in summer. This is a mom&pop style small shop, which means customer satisfactory is crucial to its survival.
Recently, some customers complain that waiting time is too long, and they are unhappy to stand in the sun especially in summer. This ice-cream shop doesn't have extra cash flow
to rent a bigger place for customers to sit and eat. Therefore, they think about optimizing the structure of employees to minimize the waiting time. But first they would like to find out
**whether there is a relationship between number of experienced/inexperienced chef/cashier and waiting time**.
The waiting time is referred to average waiting time of customers per day.


### Products and Constraints
**Unit equivalency:**
We assume 1 medium ice-cream ~ 1.5 small ice-cream in unit; 1 large ice-cream ~ 2 small ice-cream in unit

The shop sells three sizes of ice-cream: small, medium and large. Raw materials for all of them are the same. Ice-cream in the shop are only differ in size. 
We assume the cost of a small size ice-cream is $1, a medium size ice-cream costs $1.5 and a large size ice-cream costs $2 based on 
unit equivalency. Customers can order any number of ice-cream with different sizes as
long as the raw material in the shop is enough. When the shop runs out of raw material it will stop taking new orders but will complete the orders that have been ordered before. 

The operation simulation also takes employee salaries into consideration. All employees are hourly paid, and if the salary expense for employees is larger than one day budget of the shop, the shop
has to adjust employee numbers before running simulation. It is also important that there should be at least one chef either experienced or inexperienced and one cashier either experienced or inexperienced in the shop. 
Otherwise, the simulation is not valid.


### Employee structure
There are two kinds of employees in the shop: Cashier and Chef.
Nitrogen ice-cream is different from traditional ice-cream which requires specific skills. Therefore, cashier and chef cannot switch roles when business is busy.

![alt text](http://images.honestcooking.com/wp-content/uploads/2012/06/Milk-Solid-Ice-Cream-Bangkok-495x316.jpg)


### Operating process
There are two operating processes in the shop: Ordering and Preparing. When customers come in, cashier will serve them first. Cashier will record the number of each size of ice-cream
the customer orders. There could be more than 1 cashier, and they will serve customers concurrently when more customers come in. 

When any of cashiers finish customers' ordering process chef will start to prepare ice-cream. There could be more than 1 chef. They will process orders concurrently. For example, if one customer orders 2 small ice-cream and 1 medium ice-cream
this customer generates 3 preparing orders. If there are 3 chef who are not busy then 3 of them will prepare these 3 orders at the same time. For fairness, if there are few customers coming in
situation won't happen that one specific chef will always work. When preparing orders come and several chef are idle, 1 of the chef will be selected randomly to work on it.


### Operating hour
The shop operates from 12PM - 10PM. This is the real operating hour of Jarling icecream shop in Champaign. We use that in our simulation. The shop will stop taking orders at 9:45PM, and
will finish the remaining orders. It happens that chef work after 10PM to process the remaining orders.


### Analytical output
We simulate the situation in time log format. In this way, people can see details about when the new customer comes in, when their orders are completed and when their ice-cream are made.
An example of time log simulation can be viewed at [Analysis of Simulation](Analysis%20of%20simulation.ipynb). People can choose to either view the time log or have an output .csv
file. There are sample output files in the repo, and our statistical analysis uses these data.


## Simulation's variables of uncertainty

1. Ice-cream: Number of ice-cream for each size ordered by customers (normal discrete distribution)
              
      Number of ice-cream is discrete.
              
2. Customer: Ordering time (normal distribution) 

      Parents with kids might take longer time to order as they got distracted by kids frequently. Elderly people speak slowly to order.
      Young people might speak faster and finish ordering quicker. In this shop, most customers are young people since they like to go out.

3. Customer: Thinking time (uniform distribution) 
      
      This is a mom&pop shop, and many of the customers are regular ones. They usually don't take much time to order.
      Besides, there are only three sizes of ice-cream to choose. It shouldn't take much time to think about what to order even for new customers.

4. Chef: Preparation time based on various levels of experience (normal distribution)

5. Cashier: Preparation time based on various levels of experience (normal distribution)

6. Customer arrival: Whether there is a customer coming in each second. (Bernoulli distribution)
                              
      We assume the probability of a customer comes in per second during rush hour is (1/240); the probability of a customer comes in per second during non-rush hour is (1/1200).


## Hypothesis or hypotheses before running the simulation:
*NULL Hypothesis*: Average waiting time has no association with the number of experienced chef, the number of inexperienced chef, the number of experienced cashier, the number of inexperienced cashier.

*Alternative Hypothesis*: At least one of the variables (the number of experienced chef, the number of inexperienced chef, the number of experienced cashier, the number of inexperienced cashier) has association with average waiting time.

![waiting line](https://github.com/sayaaoi/Final_Project/blob/master/data/waiting%20line.png)

## Analytical Summary of our findings:
We control the number of budget and raw material cost, and run simulation program to generate sample data. 
We then fit a linear regression model based on findings from data exploration, and adjust model according to statistical output.

### Conclusion

Number of experienced chef, inexperienced chef has association with average waiting time while experienced cashier, inexperienced cashier don't have significant association
with average waiting time given 95% confidence interval.

## Instructions on how to use the program:
 - *Simulation*: Put [Customer](Customer.py), [Employee](Employee.py), [Distribution](Distribution.py), [Operation](Operation.py), [icshop_simulation](icshop_simulation.py) and [Data](data) 
 under the same folder. Then run [icshop_simulation](icshop_simulation.py)   
          
     The program will show time stamp of operations in console. Feel free to try different parameters.
     
     Parameters include: 
     ````
     1. Number of experienced chef 
     2. Number of inexperienced chef 
     3. Number of experienced cashier 
     4. Number of inexperienced cashier 
     5. Budget 
     6. Raw material cost 
     7. Filename (name of the output file if timelog is False)
     8. Timelog (show time stamp or not: bool) 
     ````
     Output file will include the following information:
     ````
     1. Number of experienced chef
     2. Number of inperienced chef
     3. Number of experienced cashier
     4. Number of inperienced cashier
     5. Total number of small ice-cream
     6. Total number of medium ice-cream
     7. Total number of large ice-cream
     8. Total number of ice-cream based on unit equivalency
     9. Number of customer
     10. Average ordering time
     11. Average preparing time
     12. Average waiting time
     13. Profit

 - *Data exploration*: [Data Visualization](Analysis%20of%20simulation.ipynb)   
          
    You need to have [Simulation Program](icshop_simulation.py) under the same folder in order to replicate the result in the notebook.
    There are demo of time log simulation result, plots of waiting time with different combinations of employees, plots of profit with different combinations of employees

 - *Data analysis*: [Data Analysis](Data_Analysis.md)
                 
      Summary/graph statistics -> fit linear regression model -> transform the model -> interpret model -> come to conclusion

## All Sources Used:
- Miller & Ranum: Problem Solving with Algorithms and Data Structures Using Python, Section 3.4, pages 106-119
- [How to put legend out of the plot](https://stackoverflow.com/questions/4700614/how-to-put-the-legend-out-of-the-plot?)
- [Bash Color functions](https://gist.github.com/daytonn/8677243)
- [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#blockquotes)
- https://github.com/nikolausn/Final-project



