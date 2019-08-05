### pypattyrn
---
https://github.com/tylerlaberge/PyPattyrn

```py
from pypattyrn.creational.singleton import Singleton
class DummyClass(object, metaclass=Singleton):

from pypattyrn.behavioral.chain import Chain, ChainLink

class ConcreteChainLinkThree(ChainLink):
  def handle(self, request):
    if request == 'handle_three':
      return "Handled in chain link three"
    else:
      return self.successor_handle(request)
      
class ConcreateChainLinkTwo(ChainLink):
  def __init__(self):
    super().__init__()
    self.set_successor(ConcreateChainLinkThree())
    
  def handle(self, request):
    if request == 'handle_two':
      return "Handled in chain link two"
    else:
      return self.successor_handle(request)
      
class ConcreateChainLinkOne(ChainLink):
  def __init__(self):
    super().__init__()

```

```sh
pip install pypattyrn
git clone https://github.com/tylerlaberge/PyPattyrn.git
cd PyPattyrn
python setup.py install
```

```
```


