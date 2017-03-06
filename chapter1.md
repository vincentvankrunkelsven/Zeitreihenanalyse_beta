---
title       : Section 1 Introduction to Time Series
description : Exercises accompanying section 1 of the lecture

--- type:NormalExercise lang:r xp:100 skills:1 key:977a73283d
## Discoveries


The `discoveries` data set contains the numbers of "great" inventions and scientific discoveries in each year from 1860 to 1959.
It is also one of the many data sets which are immediately available after the installation of `R`.
Type `data()` in the R console on your computer to find others (this does not work in DataCamp). 

Your task is to conduct a rudimentary analysis of this data set while you will learn some of the basics of working with time series in `R`. 


*** =instructions
- Print out the time series `discoveries` and examine the output. 
- Find out of how many observations this time series consists.  Use `length()` to achieve this. 
- Print out the first 6 and the last 7 observations. Use `head()` and `tail()` for this. 
- Visualize the time series using the `plot()` function.  

*** =hint
- You can print something by either using to function `print()` or by just typing the name of the object you want to print. 
- You can always use the `R` `help()` function. For example,`help(head)` or `?head`. 
- When working with time series data it is enough to call `plot()` with the time series object as its only argument to generate a decent plot.  


*** =pre_exercise_code
```{r}
library(xts)
```

*** =sample_code
```{r}
# 1. Print the time series


# 2. Compute the length of the time series


# 3. Print the first 6 and the last 7 observations 


# 4. Generate a plot


```

*** =solution
```{r}
# 1. Print the time series
print(discoveries)

# 2. Compute the length of the time series
length(discoveries)

# 3. Save the first 6 and the last 7 observations 
head(discoveries)
tail(discoveries, n = 7)

# 4. Generate a plot
plot(discoveries)
```

*** =sct
```{r}
ex() %>% check_output_expr("print(discoveries)", missing_msg  = "Did you print out the time series?")
ex() %>% check_function("length") %>%  check_result() %>% check_equal()
ex() %>% check_function("head") %>%  check_result() %>% check_equal()
ex() %>% check_function("tail") %>%  check_result() %>% check_equal()
ex() %>% check_function("plot") %>% check_arg("x") %>% check_equal()
```

--- type:NormalExercise lang:r xp:50 skills:1 key:d6643423b8
## Create a time series

In the previous excercise a proper time series was already provided. 
Mostly this will not be the case.
Assume we observed for each day of the week how many students were in the university canteen.

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-yw4l{vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-yw4l">Mon.</th>
    <th class="tg-yw4l">Tues.</th>
    <th class="tg-yw4l">Wed.</th>
    <th class="tg-yw4l">Thurs.</th>
    <th class="tg-yw4l">Fri.</th>
  </tr>
  <tr>
    <td class="tg-yw4l">2500</td>
    <td class="tg-yw4l">4000</td>
    <td class="tg-yw4l">4500</td>
    <td class="tg-yw4l">4250</td>
    <td class="tg-yw4l">500</td>
  </tr>
</table>

<br>
From the data in this table we want to create a simple time series object in R. 

*** =instructions

- Create a simple vector called `vec` containing the numbers from the table. 
- Use the function `ts()` to create a time series object from `vec` and assign the result to `ts_vec`.
- Find out to what kind of class `vec` and `ts_vec` belong to. Use `class()` for this task. 

*** =hint
You can use`c()` to **c**ombine values to a vector. 


*** =sample_code
```{r}
# Create vec


# Create ts_vec


# Print out the class of vec and ts_vec

```

*** =solution
```{r}
# Create vec
vec    <- c(2500, 4000, 4500, 4250, 500)

# Create ts_vec
ts_vec <- ts(vec)

# Print out the class of vec and ts_vec
class(vec)
class(ts_vec)

```

*** =sct
```{r}
ex() %>% check_object("vec") %>% check_equal()
ex() %>% check_function("class", index = 1) %>% check_arg("x") %>% check_equal()
ex() %>% check_function("class", index = 2) %>% check_arg("x") %>% check_equal()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:a24b9395c7
## Why using class ts?

In R each object has a class. Along with the now introduced class `ts` 
you might already know the classes `vector`, `matrix`, `list` 
and `data.frame` from the introduction course. 

The cool thing about classes is that they save you work. 

Everything you can do with a `ts` object can also be done with a normal vector.
So it is not mandatory to work with `ts` objects for time series analysis in R. 
However, it makes life often easier if we do so. The reason is that several 
functions such as plot behave differently depending on the class of their arguments. 

*** =instructions
- Plot `vec` and `ts_vec` one below the other. The `par()` function in the sample code
   will achieve this. Simply put the code for the two plots below. Note the difference. 

*** =hint
- You can increase the size of the plot window to get a better view on the plots you created. 


*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Generate the time series 
vec    <- c(2500, 4000, 4500, 4250, 500)
ts_vec <- ts(vec)

# Plot both objects
par(mfrow = c(2,1))
```

*** =solution
```{r}
# Generate the time series 
vec    <- c(2500, 4000, 4500, 4250, 500)
ts_vec <- ts(vec)

# Plot both objects
par(mfrow = c(2,1))
plot(vec)
plot(ts_vec)
```

*** =sct
```{r}
ex() %>% check_function("plot", index = 1) %>% check_arg("x") %>% check_equal()
ex() %>% check_function("plot", index = 2) %>% check_arg("x") %>% check_equal()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:540490b825
## Quarterly Data
You already know some basics about time series objects of class `ts`. Now, we
want to create a time series for which we have to define more than just one argument 
of the function `ts()`.

We want to create a quarterly time series which starts in the 3. quarter of the year
2000. This can be done by calling `ts()` with the additional arguments `start` and `frequency`. 
`start` will tell the time series when to start. `frequency` defines how many observations 
occur per unit of time (in our case per year). 

If we for example want the series to start
in the 4. quarter 2016 than we would have to type `ts(x, start = c(2016, 4), frequency = 4)`.
We set frequency to `4` because a year consists of `4` quarters. For monthly data we would have
`frequency = 12` and so on. 



*** =instructions

  -  Create a time series which starts in the 3. quarter of the year 2000 and assign it to `x_ts`. Use the observations contained in the variable `x`.
  -  Print out the time series to the console and produce a simple plot.

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
# Generating sample data
set.seed(123)
x <- sample(0:100, size = 50, replace = TRUE) 

# Create the time series object


# Print the time series 


# Plot the time series 
```

*** =solution
```{r}
# Generating sample data
set.seed(123)
x <- sample(0:100, size = 50, replace = TRUE)  

# Create the time series object
x_ts <- ts(x, start = c(2000, 4), frequency = 4)

# Print the time series 
x_ts

# Plot the time series
plot(x_ts)

```

*** =sct
```{r}
ex() %>% check_object("x_ts") %>% check_equal()
ex() %>% check_output_expr("x_ts")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:008b4c5172
## Subsetting a Time Series

Another data set directly available in R is the `AirPassanger` data set.
It contains the number of air passangers in the first years of commercial aviation. 

We are only interested in the first $4$ years. Therefore we want to subset the 
original time series and save it as a new object. A convinient way of subsetting 
time series is the function `window()`. We provide the original time series as well as
the start and the end date of the desired subset 
(e.g. for a monthly time series `window(TimeSeries, start = c(year, month), end = c(year, month) )`).
One advantage of `window()` is that in contrast to other subsetting techniques an object of class `ts` is returned.  

First, we need to figure out when the time series starts and what frequency it has in order to 
provide sensible dates. Then we can use the `window()` function for subsetting. 
Finally, we will create an object with the remaining years. 


*** =instructions
- Plot the time series `AirPassangers`. This object is already available in your enviornment. 
- When does the time series start and when does it end? Use `start()` and `end()` to find it out. 
- What is the underlying frequency? Use `frequency()` to get the answer. 
- Create a new object called `AP_begin` with only the first 4 years of the original time series. Print out `AP_begin`! 
- Create a new object called `AP_rest` with the remaining years. Print out `AP_rest`!

*** =sample_code
```{r}
# Plot the AirPassanger time series


# Find out the start and the end date 


# Determine the frequnecy


# Create and print vector containing only the first 4 years



# Create and print containing the remaining series



```

*** =solution
```{r}
# Plot the AirPassanger time series
plot(AirPassengers)

# Find out the start and the end date 
start(AirPassengers)
end(AirPassengers)

# Determine the frequnecy
frequency(AirPassengers)

# Create and print out a vector containing only the first 4 years
AP_begin<- window(AirPassengers, start =  start(AirPassengers), end = c(1952, 12))
AP_begin

# Create and print out a vector containing the remaining series
AP_rest <- window(AirPassengers, start = c(1953, 1), end =  end(AirPassengers))
AP_rest

```
*** =sct
```{r}
ex() %>% check_function("plot") %>% check_arg("x") %>% check_equal()
ex() %>% check_function("start") %>% check_arg("x") %>% check_equal()
ex() %>% check_function("end") %>% check_arg("x") %>% check_equal()
ex() %>% check_function("frequency") %>% check_arg("x") %>% check_equal()
ex() %>% check_function("window", index = 1) %>% check_result() %>% check_equal()
ex() %>% check_function("window", index = 2) %>% check_result() %>% check_equal()
ex() %>% check_object("AP_begin")  %>% check_equal()
ex() %>% check_object("AP_rest")  %>% check_equal()
ex() %>% check_output_expr("AP_begin")
ex() %>% check_output_expr("AP_rest")
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:89fdfcd16b
## Properties of the AirPassanger time series
With your knowledge about stationarity and how a stationary process should look like reconsider the `AirPassanger` time series. 
Which of the following statements are true?

<ol>
  <li>Looks like a random walk.</li>
  <li>The time series has a time trend. </li>
  <li>It could be white noise. </li>
  <li>The time series exhibits a seasonal pattern. </li>
  <li>The seasonal pattern gets stronger with increasing $t$.</li>
  <li>The underlying process seems to be perfectly stationary.</li>
</ol>

You need to find all true statements. 

*** =instructions
- The statements 1, 3, 6 are true. 
- The statements 2 and 5 are true.
- Only statements 6 is true.
- The statements 2, 4, and 5 are true.  
- Only statements 4 is true.
- The statements 1, 2, and 4 are true.
- All statements but 6 are true. 

*** =hint

*** =pre_exercise_code
```{r}
plot(AirPassengers)
```

*** =sct
```{r}
test_mc(correct = 4)
```
--- type:NormalExercise lang:r xp:100 skills:1 key:f3288cd690
## Trend and Seasonality I

In the near future we will consider ARMA - models which can be applied only to stationary processes. 
As we found in the previous exercise, the `AirPassanger` time series is clearly not stationry. 
To work with this kind of model we need to transform the original time series in a stationary one. 

In our case this means that we have to remove the time trend and the seasonal pattern. In the lecture several methods 
were discussed how you can achieve this. In the exercise session those methods will be considered in much more 
detail. 

Here we will introduce the R function `decompose()`. `decompose()` does not require any knowledge about the 
underlying methods, which makes it an easy to use function. However, when applied without caution it can yield misleading results. 

`decompose()` assumes the following model: 

$$Y _t = s _t + m _t + X _t,$$

where $s _t$ is the seasonal component, $m _t$ is the trend component and $X _t$ is the random component. 
`decompose()` uses moving average filters to estimate $s _t$ and $m _t$. 

In order to use `decompose()` you need an object of type `ts` with `frequency > 1`. When working with real data
make sure to check this condition. 


*** =instructions
- Apply `decompose()` to `AirPassangers` and assign the results to `AP_decomp`.
- Plot `AP_decomp` and inspect the output. 
- Extract only the seasonal component form `AP_decomp` and save it as `AP_seasonal `. `?decompose` is helpful here. Look for the caption "Value". This section describes the output object of a function.  
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
#Decompose the AirPassangers time series


#Visualize the decomposed time series


#Extract the seasonal component


#Plot only the seasonal component


```

*** =solution
```{r}
#Decompose the AirPassangers time series
AP_decomp <- decompose(AirPassengers)

#Visualize the decomposed time series
plot(AP_decomp)

#Extract the seasonal component
AP_seasonal <- AP_decomp$seasonal

#Plot only the seasonal component
plot(AP_seasonal)
```

*** =sct
```{r}
ex() %>% check_object("AP_decomp") %>% check_equal()
ex() %>% check_function("plot", index = 1) %>% check_arg("x") %>% check_equal()
ex() %>% check_object("AP_seasonal") %>% check_equal()
ex() %>% check_function("plot", index = 2) %>% check_arg("x") %>% check_equal()
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:8274a78ae5
## Trend and Seasonality II

Reconsider the seasonal decompositon provided by `decompose()`. 
What do you think about the result?

*** =instructions

- It looks good. The random component moves arround $0$. We can start working with ARMA models. 
- The random model still has a distinct pattern and does not appear to be stationary. We have to reconsider our approach.  

*** =hint

*** =pre_exercise_code
```{r}
#Decompose the AirPassangers time series
AP_decomp <- decompose(AirPassengers)

#Visualize the decomposed time series
plot(AP_decomp)
```

*** =sct
```{r}
test_mc(2)
```





--- type:NormalExercise lang:r xp:100 skills:1 key:0fa3f21fde
## Trend and Seasonality III

Why did it not work as expected? 

As already stated decompose assumes a model of the form:

$$Y _t = s _t + m _t + X _t.$$

However, we found earlier that the seasonal pattern becomes stronger with increasing level of the time series. 
The simple model assumed by `decompose()` considers the seasonal pattern $s_t$ to be constant over time.

One way to improve our results is to take logarithms.  


*** =instructions

- Take the logarithm of the time series and assign it to `AP_logs`.
- Plot `AP_logs`. Can you see what changed?
- `decompose()` `AP_log` and assign the result to `AP_log_decomp`. Plot `AP_log_decomp`.
- What do you think about the result?

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
#Take the logarithm 

 
#Plot


#Decompose and plot


```

*** =solution
```{r}
#Take the logarithm 
AP_log <- log(AirPassengers)
 
#Plot
plot(AP_log)

#Decompose and plot
AP_log_decomp <- decompose(AP_log)
plot(AP_log_decomp)

```

*** =sct
```{r}
ex() %>% check_object("AP_log") %>% check_equal()
ex() %>% check_function("plot", index = 1) %>% check_arg("x") %>% check_equal()
ex() %>% check_object("AP_log_decomp") %>% check_equal()
ex() %>% check_function("plot", index = 2) %>% check_arg("x") %>% check_equal()
```
--- type:NormalExercise lang:r xp:100 skills:1 key:cec3a5d183
## Aggregate
The `AirPassanger` series has both an upward sloping trend and a seasonal pattern. 
We can extract the trend by considering the monthly average of each year. 

To achieve this the function `aggregate()` can be used. This function takes two inputs: a time series and 
a function. The function is applied to all values of each year (time unit).
So if we have a time series with monthly data beginning in January 2000 and ending in December 2001
the function will be applied to the $12$ values of the year $2000$ and the $12$ values of the year 2001. 
By default `aggregate()` computes the sum of all values belonging to one time unit. 
In our case we are however interested in the average for which we can use `mean()`. 

The function call you need should be of the form `aggregate(TimeSeries, FUN = "functionName")`. Do not forget 
the `" "` arround the name of the function you want to apply. 




*** =instructions
- Compute the monthly average of each year with `aggregate()`. Assign the result to the variable `AP_avg`. 
- Produce a plot of the original time series and add a red line with the values of `AP_avg` to the plot. You can use 
  the function `lines()` where you set the argument `col` to `"red"`. If you get the error: "Error: plot.new has not been called yet" you
  have to run the call to `plot()` and `lines()` in one block. 



*** =hint

*** =pre_exercise_code
```{r}
plot(AirPassengers)
```

*** =sample_code
```{r}
#Compute monthly average per year


#Add the average to the plot

```

*** =solution
```{r}
#Compute monthly average per year
AP_avg <- aggregate(AirPassengers, FUN =  "mean")

#Add the average to the plot
plot(AirPassengers)
lines(AP_avg, col = "red")
```

*** =sct
```{r}
ex() %>% check_object("AP_avg") %>% check_equal()
ex() %>% check_function("plot") %>% check_arg("x") %>% check_equal()
fun_lines <- ex() %>% check_function("lines")
fun_lines %>% check_arg("x") %>% check_equal()
fun_lines %>% check_arg("col") %>% check_equal()

```
--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:06d273312f
## Sequence of random variables 
For the next excercises the lecture script will be helpful. Try to understand the meaning of the answers. 

How do we call an ordered sequence of random variables (rv) which are defined on the same probability space?  

*** =instructions
- random walk
- AR-process
- (discrete) stochastic process
- martingale 


*** =sct
```{r}
test_mc(correct = 3)
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:2c1f9e3f09
## Time Series
How can a time series be defined?

*** =instructions

- As a (discrete) stochastic process. 
- As a realization of a (discrete) stochastic process. 
- As a sequence of variables.
- As a process in continues time.


*** =sct
```{r}
test_mc(correct = 2)
```
--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:feab989ec6
## (Weak) Stationarity

We say a time series process is weakly stationary if: 

*** =instructions
- The mean is constant over time.
- The autocovariances do not depend on $t$.
- The process stays within a certain interval.
- The first two moments do not change over time.


*** =sct
```{r}
test_mc(correct = 4)
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:5283338175
## Ergodicity

The time series process $\\{Y_t\\}$ is ergodic if 

$$\overline{Y}_T =\frac{1}{T} \sum^T _{t = 1} y _t$$

*** =instructions
- converges to the sample mean.
- converges to $\mu$ as $T \rightarrow 0$.
- converges to $0$ as $T \rightarrow \infty$.
- converges to $E[Y_t]$ as $T \rightarrow \infty$.

*** =sct
```{r}
test_mc(correct = 4)
```
--- type:NormalExercise lang:r xp:100 skills:1 key:7a727ce4c0
## Gaussian White Noise Process
In this exercise we use `R` to generate a simple time series from a Gaussian White Noise Process. R provides random number generators which make it easy 
to draw random numbers from a variety of probability distributions. 

*** =instructions
- Set the seed to `123`. 
- Assign to the variable `y` a realization of a Gaussian White Noise Process with $\sigma = 1.4$ and $100$ observations. `y` should be of class `ts`. 
- Create a simple plot of `y`. 


*** =hint
- With `set.seed(123)` you always get the same realizations of your random variables (stochastic processes) 
  which makes your code reproducible. 
- You can use `rnorm()` to generate numbers from a normal distribution. 

*** =sample_code
```{r}
# 1. Set the seed


# 2. Generate the process


# 3. Plot the time series
```

*** =solution
```{r}
# 1. Set the seed
set.seed(123)

# 2. Generate the process
y <- ts(rnorm(100, sd = 1.4))

# 3. Plot the time series 
plot(y)
```

*** =sct
```{r}
test_student_typed("set.seed(123)",
                   fixed = TRUE,
                   times = 1,
                   not_typed_msg = "Did you set the seed?")
                   
test_object("y",
            eq_condition = "equivalent",
            eval = TRUE,
            undefined_msg = "Did you assign the process to the variable `y`?",
            incorrect_msg = "The random process you created does not match the requirements stated in the instructions")
            
 fun <- ex() %>% check_function('plot', not_called_msg = "Please use `plot()` to produce a scatterplot.")
 fun %>% check_arg("x") %>% check_equal()
 # add type = "p" as a correct solution
```

--- type:NormalExercise lang:r xp:100 skills:1 key:01b31c2e4d
## Sligthly more complicated process

In this exercise you have to generate a time series from a sligthly more complicated process.
Here we make use of the fact that `rnorm()` is a vectorized function. (What does this mean?)

*** =instructions
- set the seed to 123
- generate a realization of the process 
  $$Y_t = 4 + \epsilon _t \text{, } \,\,\,\,\,\, \epsilon _t \sim N(0,t)$$ for $t _1 = 1, t _2 = 2 ,…,t _{100} = 100$
  and assign it to the variable `y` which should have class `ts`.
- Plot the time series.


*** =hint
- It might be helpful to create a vector containing the time indices which you can pass to `rnorm()`.
- The internet is a great source for R related questions. One very helpful site is [Stack Overflow](http://stackoverflow.com/questions/3510619/calling-rnorm-with-a-vector-of-means).
Most problems you might encouter should have been already answerd there. The trick is to identify the right question.   

*** =solution
```{r}
set.seed(123)
# vector of time indices
t <- 1:100
# generate the time series
y <- ts(rnorm(100, mean = 4, sd = t))

#plot the time series
plot(y)
```

*** =sct
```{r}
test_student_typed("set.seed(123)",
                   fixed = TRUE,
                   times = 1,
                   not_typed_msg = "Did you set the seed?")

ex() %>% check_object("y") %>% check_equal()       
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:db72c3ec1f
## Is this process stationary? 

Consider the process from the previous exercise
$$Y_t = 4 + \epsilon _t \text{, } \,\,\,\,\,\, \epsilon _t \sim N(0,t)$$

Is $\{Y_t\}$ stationary?


*** =instructions

- Yes, because the mean does not change over time.
- No, because the mean changes over time. 
- No, because the second moments converge to $0$.
- No, because $\sigma _t \neq \sigma _{t+1}$.
- Yes, because the process is ergodic.

*** =hint

*** =pre_exercise_code
```{r}
set.seed(123)
t <- 1:100
y <- 4 + rnorm(100, sd = t)
plot(y ~ t, type = "l")
```

*** =sct
```{r}
test_mc(correct = 4)
```

--- type:NormalExercise lang:r xp:100 skills:1 key:690fce9e08
## Autocorrelation

Autocorrelation is the correlation of one variable with itself at different points in time.
As you will see in the next lectures, the autocorrelation structure can provide useful information about the underlying stochastic process. 
The function `acf()` computes by default $ \hat{\rho _1}, \ldots, \hat{\rho} _{30} $. If you want to compute a different number of autocorrelations check out 
the help page.

The default output of `acf()` is a barplot. If you are interested in the numbers you can either wrap the call to `acf()` in a call to print (i.e. `print(acf(x))`)
or assign the result to a new variable (i.e. `auto_cor <- acf(x) `). The new varaible behaves similar to a normal vector. Hence you can use regular subsetting.  


*** =instructions
- The time series `ts` is already loaded into the workspace. 
- Plot the empirical autocorrelation function of `ts`.
- Compute the first two autocorrelation coefficients $\hat{\rho _1}$ and $ \hat{\rho} _2$ and store them in the variables `rho1` and `rho2`.

*** =hint
 

*** =pre_exercise_code
```{r}
set.seed(123)
ts <- arima.sim(list (ar = 0.9), n = 1000)
```

*** =sample_code
```{r}
#Plot the autocorrelations


#Create rho1 and rho2



#Print rho1 and rho2

```

*** =solution
```{r}
#Plot the autocorrelations 
acf(ts)

#Create rho1 and rho2
auto_cor <- acf(ts)
rho1 <- auto_cor[2]
rho2 <- auto_cor[3]

#Print rho1 and rho2
rho1
rho2
```

*** =sct
```{r}
  fun <- ex() %>% check_function("acf")
  fun %>% check_arg("x") %>% check_equal()
  
test_object("rho1",
            eq_condition = "equivalent",
            eval = TRUE)
    
            
test_object("rho2",
            eq_condition = "equivalent",
            eval = TRUE)

ex() %>% check_output_expr("rho1") 
ex() %>% check_output_expr("rho2") 
```

