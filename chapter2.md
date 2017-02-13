---
title       : Section 2 ARMA Models
description : Insert the chapter description here

--- type:NormalExercise lang:r xp:100 skills:1 key:ff2014d23c
## Simulate from a MA(q) processes

In the lecture you learnt about Moving Average (MA) processes of the form 

$$Y _t = \mu + \sum _{j = 0} ^q \theta _j \epsilon _{t-j}.$$

The function `arima.sim()` can be used to simulate time series from an underlying MA process. 
In order to generate 100 data points from the $MA(2)$ process 

$$Y _t = 2 + \epsilon _{t} + 0.6 \epsilon _{t-1} - 1.5 \epsilon _{t-2} $$

we would type: `arima.sim(model = list(ma = c(0.6, -1.5)), mean = 2, n = 100)`.




*** =instructions
- Set the seed to 123.
- Generate 1000 observations from a Gausian White Noise Process. Use `arima.sim()` for this and assign the result to the variable `wn`.
- Generate 1000 observations form the process $$Y _t = 7 + \epsilon _{t} - 1.5 \epsilon _{t-1} $$ and assign the result to the variable `ma1`.
- Generate 1000 observations from the process $$Y _t = \epsilon _{t} + \epsilon _{t-1} + \epsilon _{t-2} + + \epsilon _{t-3} + \epsilon _{t-4} + \epsilon _{t-5}$$ and assign the result to the variable `ma5`.
- Plot `wn`, `ma_1` and `ma_5` below each other and examine the characteristics of the time series.  


*** =hint
- To simulate a White Noise process you can pass an empty list (`list()` produces an empty list) to the `model` argument  .


*** =sample_code
```{r}
#Set the seed

#Simulate the time series

#Plot all three time series
par(mfrow = c(3,1))
```

*** =solution
```{r}
#Set the seed
set.seed(123)
#Simulate the time series
wn    <- arima.sim(model = list(), n = 1000 )
ma_1  <- arima.sim(model = list(ma = c(1)), n = 1000 )
ma_5  <- arima.sim(model = list(ma = c(1,1,1,1,1) ), n = 1000 )
#Plot all three time series
par(mfrow = c(3,1))
plot(wn)
plot(ma_1)
plot(ma_5)
```

*** =sct
```{r}
ex() %>% check_object("wn") %>% check_equal()
ex() %>% check_object("ma_1") %>% check_equal()
ex() %>% check_object("ma_5") %>% check_equal()
ex() %>% check_function('plot', index = 1) %>% check_arg("x") %>% check_equal()
ex() %>% check_function('plot', index = 2) %>% check_arg("x") %>% check_equal()
ex() %>% check_function('plot', index = 3) %>% check_arg("x") %>% check_equal()
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:f0a5b6291d
## Compare Variance of WN and MA process

What can you say about the variances of the processes $Y _t$ and $Z _t$? 

$$ Y _t = \epsilon _t $$
$$ Z _t = \epsilon _t + 0.9 \epsilon _{t-1} $$
$$\epsilon _t \sim (0, \sigma)$$


*** =instructions
- The variance of $Y_t$ is larger because a white noise process is more wiggly than an $MA$ process.
- The variance of $Y_t$ is larger because $Z _t$ is a smoothed version of $Y _t$.
- The variance of $Z _t$ is larger because $$Var(Z _t) = \sigma^2 (1 + \theta^2) $$.
- The variance of $Z _t$ is larger because there are positive autocovariances. 

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}
test_mc(correct = 3)
```
--- type:NormalExercise lang:r xp:100 skills:1 key:40dfa9e855
## Simulate form an AR(p) processes

Now we want to use `arima.sim()` to generate time series from an $AR$ process. 
Consider the process:
$$Y_t = 0.4 Y _{t-1} + 0.2 Y _{t-2} + \epsilon _t.$$

We can simulate one possible path of this process with 100 observation by typing
`arima.sim(ar = c(0.4, 0.2), n = 100)`.


*** =instructions
- Set the seed to 123
- Simulate 1000 observations of the process $$Y_ t = 0.9 Y_ {t-1} + \epsilon_ t$$ and save the result to the variable `ar_1`. 
- Compare it to the realizations of the White Noise and the $MA(5)$ process from the previous question by plotting the 3 time series.  

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
#Set the seed
set.seed(123)
#Simulate the time series
wn    <- arima.sim(model = list(), n = 1000 )
ma_5  <- arima.sim(model = list(ma = c(1,1,1,1,1)), n = 1000 )


#Plot all three time series
par(mfrow = c(3,1))
plot(wn)
plot(ma_1)
```

*** =solution
```{r}
#Set the seed
set.seed(123)
#Simulate the time series
wn    <- arima.sim(model = list(), n = 1000 )
ma_5  <- arima.sim(model = list(ma = c(1,1,1,1,1)), n = 1000 )
ar_1  <- arima.sim(model = list(ar = 0.9), n = 1000)

#Plot all three time series
par(mfrow = c(3,1))
plot(wn)
plot(ma_5)
plot(ar_1)
```

*** =sct
```{r}
ex() %>% check_object("ar_1") %>% check_equal()
ex() %>% check_function("plot") %>% check_arg("x") %>% check_equal()
```






--- type:NormalExercise lang:r xp:100 skills:1 key:73d56a11ab
## Simulate from an ARMA(p,q) process

To generate a time series from an $ARMA(p,q)$ process we pass both
$AR$ and $MA$ coefficients to `arima.sim()`.

To simulate 200 observations from the process

$$Y _t = 2.7 + 0.5 Y _{t-1} +  0.2 Y _{t-2} + 0.7 \epsilon _{t-1} + \epsilon _t$$

we can type: `arima.sim(model = list(ar = c(0.5, 0.2), ma = 0.7), mean = 2.7, n = 200)`.

When using `arima.sim()` to simulate from a $MA(q)$ or White Noise process the argument mean corresponds to the expectation of the process $\mu$.
In case you want to simulate from an $AR(p)$ or an $ARMA(p,q)$ process `mean` corresponds to the constant $c \neq \mu$.



*** =instructions
- Set the seed to 123
- Simulate 1000 observations of a Gaussian White Noise process and assign the result to `wn`.   
- Simulate one trajectory consisting of 1000 observations of $$Y _t = 4 + 0.7 Y _{t-1} + 0.4 \epsilon _{t-1} + \epsilon _{t}$$ and assign the result to `y`.
- Plot both time series. 

*** =hint

*** =pre_exercise_code
```{r}
#set the seen 

#simulate from gaussian white noise process

#simulate from arma(1,1) process

#plot wn and y 
par(mfrow = c(2,1))





```

*** =sample_code
```{r}

```

*** =solution
```{r}
#set the seed 
set.seed(123)
#simulate from gaussian white noise process
wn  <- arima.sim(model = list(), n = 1000)
#simulate from arma(1,1) process
y <- arima.sim(model = list(ar = 0.7, ma = 0.4), mean = 4, n = 1000)
#plot wn and y 
par(mfrow = c(2,1))
plot(wn)
plot(y)
```

*** =sct
```{r}
ex() %>% check_function("set.seed") %>% check_arg("seed") %>% check_equal()
ex() %>% check_object("wn") %>% check_equal()
ex() %>% check_object("y") %>% check_equal()
ex() %>% check_function("plot", index = 1) %>% check_arg("x") %>% check_equal()
ex() %>% check_function("plot", index = 2) %>% check_arg("x") %>% check_equal()
```
--- type:NormalExercise lang:r xp:100 skills:1 key:0f12c1343e
## Empirical Autocorrelation Function 

The empirical autocorrelation functions of White Noise, $MA$ and $AR$ processes exhibit a distinct pattern which can help you in empirical applications with the model choice. 

If the 4 plots do not fit on your display or are too small you can copy and paste the code into the R console on your computer. 

*** =instructions
- Plot for each of the provided time series the empirical autocorrelation function. Use `acf` to achive this.
- Take a close look at how the different autocorrelation functions look like. 
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
#Generate time series 
wn   <-  arima.sim(model = list(), n = 10000)
ma   <-  arima.sim(model = list(ma = 0.4), n = 10000)
ar   <-  arima.sim(model = list(ar = 0.7), n = 10000)
arma <-  arima.sim(model = list(ar = 0.7, ma = 0.4), n = 10000)
#Plot autocorrelation functions
par(mfrow = c(4,1))
```

*** =solution
```{r}
#Generate time series 
wn   <-  arima.sim(model = list(), n = 10000)
ma   <-  arima.sim(model = list(ma = 0.4), n = 10000)
ar   <-  arima.sim(model = list(ar = 0.7), n = 10000)
arma <-  arima.sim(model = list(ar = 0.7, ma = 0.4), n = 10000)

#Plot autocorrelation functions
par(mfrow = c(4,1))
acf(wn)
acf(ma)
acf(ar)
acf(arma)
```

*** =sct
```{r}
ex() %>% check_function("acf", index = 1) %>% check_arg("x") %>% check_equal()
ex() %>% check_function("acf", index = 2) %>% check_arg("x") %>% check_equal()
ex() %>% check_function("acf", index = 3) %>% check_arg("x") %>% check_equal()
ex() %>% check_function("acf", index = 4) %>% check_arg("x") %>% check_equal()
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:be9cc23ee5
## Which ACF belongs to which process?

On the right you can find plots of 3 autocorrelation functions. 
Decide which process generated a time series with one of these functions. 


*** =instructions
- **a** was simulated from a White Noise process, **b** from an $AR$ process and **c** from a $MA$ process. 
- **a** was simulated from an $AR$ process and **b** and **c** from a $MA$ process. 
- **a** was simulated from an $AR$ process, **b** from an White Woise process and **c** from a $MA$ process. 
- **a** and **c** were simulated from an $AR$ process and **b** from a $MA$ process. 
- **a** was simulated from an $ARMA$ process, **b** from a White Noise process and **c** from an $AR$ process. 
*** =hint

*** =pre_exercise_code
```{r}
set.seed(1)
wn <- arima.sim(model = list(), n = 1000)
ar <- arima.sim(model = list(ar = 0.9), n = 1000)
ma <- arima.sim(model = list(ma = 1), n = 1000)

par(mfrow = c(3,1))
acf(ar, main = "a")
acf(wn, main = "b")
acf(ma, main = "c")
```

*** =sct
```{r}
test_mc(correct = 1)
```




--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:b58882ded5
## Which processes are stationary? 

Decide which process is stationary.

<ol>
  <li>$ y _t = 1.4 y _{t-1} + \epsilon _t$</li>
  <li>$ y _t = 0.4 y _{t-1} + \epsilon _t$</li>
  <li>$ y _t = 0.4 y _{t-1} + 0.6 y _{t-2} + \epsilon _t$</li>
  <li>$ y _t = y _{t-1} + \epsilon _t$</li>
  <li>$ y _t = \epsilon _t + 0.4 \epsilon _{t-1}$</li>
  <li>$ y _t = \epsilon _t + 0.4 \epsilon _{t-1} + 0.6 \epsilon _{t-2}$</li>
</ol>



*** =instructions
- No process is stationary.
- All processes are stationary. 
- The processes $2$, $5$ and $6$ are stationary.
- The processes $1$, $3$ and $4$ are stationary.
- The processes $2$ and $4$ are stationary.
- Only process $5$ is stationary. 
*** =hint

*** =pre_exercise_code
```{r}

```

*** =sct
```{r}

```

--- type:NormalExercise lang:r xp:100 skills:1 key:318d64dd4c
## An AR(2) process with complex roots 

Check whether the process 

$$y _t = 1.5 y _{t-1} - .75 y _{t-2} + \epsilon _t $$ 

is stationary. 

You can use the function `polyroot()` to compute the roots of the characteristic.

*** =instructions

- Assign the coefficients of the characteristic polynomial to the vector `z`.
- Pass `z` as an argument to `polyroot()` and assign the result to the variable `roots`. 
- Compute the absolute value of the roots (`Mod()` can do this for real as well as complex numbers) and check if they lie outside the unit circle. 

*** =hint
- How does the characteristic polynomial looks like? Double check if you used the correct signs. 

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}
#Create vector z containing the coefficients of the characteristic polynomial


#Compute the roots of the characteristic polynomial 


#Compute and print out the absolute value of the roots

```

*** =solution
```{r}
#Create vector z containing the coefficients of the characteristic polynomial
z <- c(1, -1.5, 0.75)

#Compute the roots of the characteristic polynomial 
roots <- polyroot(z)

#Compute and print out the absolute value of the roots
Mod(roots) 

```

*** =sct
```{r}
ex() %>% check_object("z") %>% check_equal()
ex() %>% check_object("roots") %>% check_equal()
ex() %>% check_output_expr("Mod(roots)")
```
