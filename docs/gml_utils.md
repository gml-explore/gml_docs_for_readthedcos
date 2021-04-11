# gml toolkit 

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
