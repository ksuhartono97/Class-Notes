# Demand Forecasting
Aggregate forecast: estimate demand for a general piece of item. Because it is hard to estimate the demand for a single item. The reason why it is more accurate than individual forecast is because you will overestimate and underestimate on certain items but these cancel out because this is an aggregate.

Short term forecast: the longer the time, the more likely it is that something in the environment changes causing inaccuracies.

## Measures of forecast accuracy
MSD better than MAD. MAD is not as good because MAD is not differentiable at a point. Because sometimes when you want to solve an optimization problem you need to do a differentiation.

MAPE for same products not really necessary, mostly needed when we do evaluation on different products as the scale of difference is probably not the same.

**Bias** in forecasts:
- Usually signified by a trend (upwards trend or downwards trend)
- Caused by the forecast model ignoring some relevant elements

## Causal Models

### Linear regression
Called SSE estimators because it tries to find parameters to minimize the SSE.

Maximum-Likelihood Estimators (ML Estimators): finds parameters to maximize the likelihood of observing the sample data.

> Demand is random (stochastic) which makes it very hard to predict.  

MSE: minimized sum of squared errors.

MNL: multinomial logit


## Time Series Models
- Naive forecast: not really used, only for benchmark. too simple.
- Moving average: cannot adjust to latest trend. Cannot choose m value (window size) that is too large otherwise we ignore any existing trend in the data.

Double exponential smoothing: tao (t in greek) is the gradient of the smoothing.

Triple exponential smoothing introduces seasonality. Defined as c<sub>t</sub> where t is the time period (e.g. season or quarter). The sum of these c values should be equal to N (the total number of seasons). 

```
c<sub>1</sub> + c<sub>2</sub> + ... + c<sub>N</sub> = N
```

Mostly the same as double exponential, just need to use the deseasonalized estimates. 

Be careful with picking the value of the seasonal estimate (the c value, the formula is a bit weird for initial situation)
