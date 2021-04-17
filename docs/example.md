![gml_logo](./gml_logo.jpg)   


After preparing the data, you can use this framework as follows.
First you need to prepare a configuration file [example](./examples/example.config),and set some [parameters](./parameter_description.md)
``` python 
[para]
top_m = 2000  
top_k = 10
top_n = 1
update_proportion = -1   
optimization_threshold = -1
balance = False
learning_epoches = 500
inference_epoches = 500
learning_method = sgd
n_process = 1
out = False
```
Then, call GML as follows:
```python            
with open('variables.pkl', 'rb') as v:
    variables = pickle.load(v)
with open('features.pkl', 'rb') as f:
    features = pickle.load(f)
graph = GML.initial("alsa.config", variables, features)
graph.inference()
```