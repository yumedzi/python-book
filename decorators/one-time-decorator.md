# One-time decorator

> Interesting usecase of decorators - when you need something to be executed just once.

Haiku about subject:

> Life is beatiful
> and cruel at the very same time
> for decorator-one-timer


```python
def batterfly(f):
    print("It was nice, thank you for all..")
    return f

@batterfly
def func():
    print("Some text")
    
func()
func()
```
Output:

    It was nice, thank you for all..
    Some text
    Some text
    
Please notice that one-time action will be executed after defining of a function. 