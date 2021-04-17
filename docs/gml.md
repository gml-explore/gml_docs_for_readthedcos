# the main class of gml

### class **GML**          
The main process of progressive machine learning, which runs through Essential Support, Approximate Probability Estimation, select topm, select topk, construct subgraph, inference subgraph process   


This class currently provides the following methods:  
```python
1. evidential_support(variable_set,update_feature_set)            
```
>Function: calculate essential support  
>parameter:  
> `variable_set` - the set of target variables    
> `update_feature_set` - the set of target features    
>Return: none            
>Return type：none          

```python
2. approximate_probability_estimation(variable_set)           
```
>Function: Calculate approximate probability  
>parameter:  
> `variable_set` - the set of target variables      
>Return: none            
>Return type：none          
```python
3. select_top_m_by_es(m)         
```
>Function: Select the first m latent variables according to the calculated Evidential Support (large to small)
>parameter:  
> `m` - The number of latent variables to be selected      
>Return: a list containing m variable ids             
>Return type：list
```python
4. select_top_k_by_entropy(var_id_list, k)            
```
>Function: calculate entropy, select top_k latent variables with small entropy  
>parameter:  
> `var_id_list` - Choose range      
> · `k` - The number of latent variables to be selected      
>Return: a list containing k ids           
>Return type：list
```python
5. select_evidence(var_id)           
```
>Function: Select the edges, variables and features which needed for subsequent subgraph construction  
>parameter:  
> `var_id` - The id of the target variable    
>Return: Edges, variables and features needed for subsequent subgraph construction            
>Return type：set
```python
6. construct_subgraph(var_id)             
```
>Function: Select topk latnet variables and create subgraph  
>parameter:  
> `var_id` - The id of the target variable         
>Return: According to the factor graph requirement of numbskull,return weight, variable, factor, fmap, domain_mask, edges           
>Return type: multiple types
```python
7. inference_subgraph(var_id)             
```
>Function: inference subgraph  
>parameter:  
> `var_id` - For entity recognition, var_id is a variable id, and var_id is a set of k variables for sentiment analysis              
>Return: none            
>Return type：none          
```python
8. label(var_id_list)             
```
>Function: Compare the entropy of k latent variables, select the one with the smallest entropy and label it, and write the parameters learned from this graph back to self.features
>parameter:  
> `var_id_list` - A list of k ids, the probability corresponding to each variable is taken from variables    
>Return: No output, directly update the label and entropy in vairables, by the way, you can update observed_variables_id and potential_variables_id  
>Return type：dict
```python
9. inference()        
```
>Function: Main flow      
>parameter:  
>none            
>Return: none            
>Return type：none            
```python
10. score() [[source]]          
```
>Function: Calculate the accuracy rate, precision rate, recall rate, f1 value of inference results, etc.  
>parameter:  
> none      
>Return: none            
>Return type：none            
```python
11. save_results()  
```      
>Function: Save the variable and feature information after inference.               
>parameter:  
> none       
>Return: none                     
>Return type：none            


###  the class for Approximate Probability Estimation：  
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


###  the class for Subgraph construction:
class **ConstructSbugraph**(variables, features, balance)               
Factor graph construction class
> Parameters：  
> - `variables` – input data of gml, the variable of the factor graph.         
> - `features` –  input data of gml, The characteristics of the factor graph.           
> - `balance` –   Whether balance the labels when constructing the subgraph. If the number of evidence variable labels(the number of 0 and 1)is quite large, it is set to True, otherwise it is set to False.

This class currently provides the following methods:
```python
1. construct_subgraph(evidences)
```
>Function：A unified construct subgraph method,it is necessary to construct a factor graph containing uary factors(parameterize or not) and binary factors, and this function is called at this time.  
>Parameters：  
>`evidences ` - Variables, edges, and feature sets required when constructing factor graphs    
>Returns：the data for Numbskull inference（weight, variable, factor, fmap, domain_mask, edges_num, var_map, alpha_bound, tau_bound, weight_map_feature, sample_list, wmap, wfactor）  
>Return type：Multiple types    
###  the class for selecting evidence
> class **EvidenceSelect**(variables,features,balance,interval_evidence_count=10,subgraph_limit_num,k_hop)  
the class for selecting evidence, select evidential variables for latent variables, including two methods for selecting evidential variables, and allow users to define their own methods
>Parameters:    
> - **variables** – One of the input data of gml, the variable of the factor graph   
> - **features** –  One of the input data of gml, the feature of factor graph   
> - **interval_evidence_limit** – When dividing interval sampling evidence, the number of evidences sampled in each interval    
> - **subgraph_limit_num** –  Maximum number of variables allowed in the subgraph    
> - **each_feature_evidence_limit** –  When sampling randomly, the number of evidence for each single factor sampling    
 
This class currently provides the following methods：
```python 
1. evidence_select(var_id)
```

>Function: Provide a unified evidence selection method, which can be used to construct factor graphs containing parameterized single factor, non-parameterized single factor, and double factor. In this case, call this function.   
>Parameters：  
> `var_id` - the id of latent variable  
>Return：connected_var_set, connected_edge_set, connected_feature_set  
>Return type：set      

### the class for computing evidential support
class **EvidentialSupport**(variables,features,method,evidence_interval_count,interval_evidence_count)                
the set of computing evidential support 
>Parameters：   
> - **variables** - variables   
> - **features** - factors   
> - **method** - The method of computing    evidential support, the default value is 'regression'   
> - **evidence_interval_count** - The number of intervals, the default value is 10   
> - **interval_evidence_count** - The number of variables in each interval, the default value is 200   

This class currently provides the following methods：     
```python         
1. get_unlabeled_var_feature_evi()
```
>Function: Calculate the ratio of 0 to 1 in the evidential variables associated with each unary feature of each latent variable, and the variable id at the other end of the binary feature   
>Return : none    
>Return type : none    
```python
2. separate_feature_value()
```
>Function: Select the easy feature value of each feature for linear regression    
>Return : none  
>Return type : none  

```python
3. influence_modeling()
```
>Function: Perform linear regression on the updated feature, save all the results of the regression back to the feature, the key is 'regression'    
>Parameter：  
> `update_feature_set` - the set of updated  feature    
>Return : none    
>Return type : none  
```python
4. init_tau_and_alpha()
```
>Function: calculate tau and alpha for feature  
>Parameter：  
>`feature_set` - the set of feature_id   
>Return : none    
>Return type : none  
```python
5. computer_unary_feature_es(variable_set)
```
>Function: calculate the essential support of each latent variable in a given set of latent variables, suitable for Aspect-level sentiment analysis   
>Parameter：   
>`variable_set` - a set of latent variables  
```python    
6. evidential_support(update_feature_set,variable_set)
```
>Function: Calculate the Evidential Support of all latent variables   
>Parameter：  
>`update_feature_set` - the set of updated feature   
> `variable_set` -The set of variables to be calculated  the evidence support.   
>Return : none    
>Return type : none     
```python
7. get_dict_rel_acc()
```
>Function: Calculate the accuracy of different types of relationships     
>Return : accuracy of different types of relations  
>Return type : dict  
```python
8. construct_mass_function_for_propensity(uncertain_degree,label_prob,unlabel_prob)
```
>Function: Build a mass function for Evidential Support calculation    
>Parameter：  
> `uncertain_degree` - Feature uncertainty  
> `label_prob` - The probability of label matching, which represents the proportion of positive instances for word features and the accuracy of relationship features for relationship features  
> `unlabel_prob` - The probability of label unmatch, which represents the proportion of negative instances for word features and 1 minus the accuracy of relationship features for relationship features     
>Return : MassFunction    
>Return type : function    
```python   
9. construct_mass_function_for_ER(theta)
```
>Function: Build a mass function for Evidential Support calculation      
>Parameter：  
> `theta` - Feature uncertainty    
>Return : MassFunction    
>Return type : function  
```python
10. labeling_propensity_with_ds(massfunctions)
```
>Function: Combine different methods for different types of evidences for aspect-level sentiment analysis
>Parameter：  
> `massfunctions` -a variable corresponding massfunctions    
>Return: Summarized the calculated evidential value    
>Return type: dict  
```python
11. evidential_support_by_custom()
```
>Function: User-defined method for calculating essential support   
>Parameter：   
>`variable_set` - a set of latent variables
>Return : none    
>Return type : none    

### the class of related Linear regression
class **Regression**(each_feature_easys, n_job, effective_training_count_threshold)
The class of related Linear regression, perform linear regression on all features, used for the essential support calculation of Entity Resolution
> Parameter：  
> `each_feature_easys` - The feature_value of the easy variable owned by each feature  
> `n_job` - calculate the number of threads  
> `effective_training_count_threshold `- The minimum number of effective samples, the default value is 2  

This class currently provides the following methods:
```python
1. perform()
```
>Function: Perform linear regression method, suitable for uary factor

### gml toolkit 

**gml_utils**       

gml commonly used tools, currently mainly provides the following methods: 
```python
1. load_easy_instance_from_file(filename) 
```      
>Function: load easy from csv file  
>Parameter:  
> `filename` - the path of csv file    
>Return: simple instance list  
>Return type: list
```python
2. separate_variables(variables)           
```
>Function: Divide variables into evidential variables and latent variables  
>Parameter:  
> `variables` - variables    
>Return: evidential variables list, latent variables list  
>Return type: list
```python
3. init_evidence_interval(evidence_interval_count)         
```
>Function: Initialize the evidence interval  
>Parameter:  
>`evidence_interval_count` - the number of intervals    
>Return: a list containing evidence_interval_count intervals  
>Return type: list
```python
4. init_evidence(features,evidence_interval,observed_variables_set)          
```
>Function: Add the evidence_interval attribute and the evidence_count attribute for each feature             
>Parameter:  
>`features` - features    
>`evidence_interval` - evidential interval    
> `observed_variables_set` - the set of evidential varibles    
>Return: none         
>Return type: none     
```python    
5. update_evidence(variables,features,var_id_list,evidence_interval)
```
>Function: update evidence_interval and evidence_count after label variables            
>Parameter: 
> `variables` - variables  
> `features`- features    
> `var_id_list` - Variable collection    
> `evidence_interval` - evidence_interval            
>Return: none             
>Return type: none    
```python     
6. init_bound(variables,features)
```
>Function: init para bound            
>Parameter: 
> `variables` - variables  
> `features` - features               
>Return: none             
>Return type: none       
```python  
7. update_bound(variables,features,var_id_list))
```
>Function: update tau and alpha bound after label variables            
>Parameter: 
> `variables` - variables  
> `features` - features               
> `var_id_list `- Variable collection    
>Return: none             
>Return type: none 
```python       
8. entropy(probability)
```
>Function: calculate entropy after given probability  
>Parameter:  
>`probability` - One probability or list of probabilities    
>Return: One entropy or a list of entropies  
>Return type: floating or list   
```python
9.  open_p(weight)       
```  
>Function: Calculate approximate probability 
>Parameter:  
>`weight` - Weight   
>Return: One entropy or a list of entropies  
>Return type: floating
```python
10. combine_evidences_with_ds(mass_functions, normalization)          
```
>Function: Summarize and calculate the evidential value of different sources
>Parameter:  
> `mass_functions` - mass function    
> `normalization` - Whether to normalize           
>Return: Summarized the calculated evidential value  
>Return type: list


class **Logger**(object) 
The log class is used to output the results to the file and the console at the same time. Currently, the following methods are mainly provided                        
>Parameter:   
> `object` – File object                         
```python
1. write(message) 
```
>Function:  Write to file and console at the same time             
>Parameter:  
>`message` - What's written            
>Return: none             
>Return type: none                       
