# the class for Approximate Probability Estimation：  
class **ApproximateProbabilityEstimation**(variables, features, method)        
Methods for Approximate Probability Estimation class  
>Parameters:   
>`variables` -variables    
> `features`  -features    
> `method`  -The method used to calculate the approximate probability 

This class currently provides the following methods:  
```python
1. init_binary_feature_weight(value1,value2)   
```
>Function：Set initial value of binary feature weight  
>Parameters:  
>`value1` - binary feature initial weight value 1  
>`value2` - binary feature initial weight value 2  
>Returns：binary feature weight initial value  
>Return type：dictionary
```python
2. labeling_conflict_with_ds(mass_functions)               
```
>Function：based on (D-S) theory Evidence support measurement  
>Parameters：  
> `mass_functions` - a dict for d-s
>Returns：Evidence support value  
>Return type：float
```python
3. get_pos_prob_based_relation(var_id, weight)                  
```
>Function：Calculate the proportion of positive instances in marked instances with a feature  
>Parameters：  
> `var_id `- Target variable id   
> `weight` - feature weight   
>Returns：Proportion of positive instances in marked instances with a feature  
>Return type：float  
```python
4. construct_mass_function_for_confict(uncertain_degree, pos_prob, neg_prob) 
```

>Function：Evidence support for calculating each feature connected to an unlabeled variable  
>Parameters：  
> `uncertain_degree` - Uncertainty of a feature  
> `pos_prob` - Proportion of positive instances in marked instances with a feature    
> `neg_prob` - Proportion of negative instances in marked instances with a feature        
>Returns：MassFunction function  
>Return type：function
```python
5. construct_mass_function_for_ER(alpha,tau,featureValue) ) 
```
>Function：Evidence support for calculating each feature connected to an unlabeled variable  
>Parameters：  
> `theta` - Uncertainty of a feature    
> `alpha` - Parameters after unaryfactor linear regression   
> `tau` - Parameters after unaryfactor linear regression   
> `featureValue`  - featurevalue  
> Returns：MassFunction function  
> Return type：function
```python
6. approximate_probability_estimation()(variable_set)           
```
>Function：Calculate the approximate probability of the selected topm hidden variables, used to select topk 
>Parameters：  
> `variable_set` Latent variable data set
>Return: none 
>Return type: none
```python    
7. approximate_probability_estimation_by_custom(variable_set)            
```
>Function：Calculate the approximate probability of the selected topm hidden variables, used to select topk, user-defined calculation rules  
>Parameters：  
> `variable_set` - Latent variable data set
>Return: none  
>Return type: none