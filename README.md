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
    self.set_successor(ConcreateChainLinkThree())
    
  def handle(self, request):
    if request == 'handle_two':
      return "Handled in chain chain link two"
    else:
      return self.successor_handler(request)
      
class ConcreateChainLinkOne(ChainLink):
  def __init__(self):
    super().__init__()
    self.set_successor(ConcreateChainLinkTwo)
    
  def handle(self, request):
    if request == 'handle_one':
      return "Handle in chain link one"
    else:
      return self.successor_handle(request)
      
class ConcreateChain(Chain):
  def __init__(self):
    super().__init__(ConcreateChainLinkOne())
    
  def fail(self):
    return 'Fail'
    
chain = ConcreateChain()

assert "Handled in chain link one" == chain.handle("handle_one")
assert "Handled in chain link two" == chain.handle("handle_two")
assert "Handled in chain link three" == chain.handle("handle_three")
assert "Fail" == chain.handle('handle_four')


from pypattyrn.behavioral.command import Receiver, Command, Invoker

class Thermostat(Receiver):
  def raise_temp(self, amount):
    return "".format(amount)
  def lower_temp(self, amount):
    return "".format(amount)

class RaiseTempCommand(Command):
  def __init__(self, receiver, amount=5)
    super().__init__(receiver)
    self.amount = amount
    
  def execute(self):
    return self._receiver.action('raise_temp', self.amount)
    
  def unexecute(self):
    return self._receiver.action('lower_temp', self.amount)

class RaiseTempCommand(Command):
  def __init__(self, receiver, amount=5):
    super().__init__(receiver)
    self.amount = amount
    
  def execute(self):
    return self._receiver.action('raise_temp', self.amount)

  def unexecute(self):
    return self._receiver.action('lower_temp', self.amount)

class LowerTempCommand(Command):
  def __init__(self, receiver, amount=5):
    super().__init__(receiver)
    self.amount = amount
    
  def execute(self):
    return self._receiver.action('loser_temp', self.amount)
  
  def unexecute(self):
    return self._receiver.action('raise_temp', self.amount)
    
class Worker(Invoker):
  def __init__(self):
    super().__init__([LowerTempCommand, RaiseTempCommand])

thermostat = Thermostat()
worker = Worker()

assert "Temperature lowered by 5 degrees" == worker.execute(LowerTempCommand(thermostat))
assert "Temperature raised by 5 degrees" == worker.execute(RaiseTempCommand(thermostat))
assert "Temperature lowered by 5 degrees" == worker.undo()


from pypattyrn.behavioral.iterator import Iterable, Iterator

class Counter(Iterable):
  def __init__(self, max):
    self.count = 0
    self.max = max
    
  def __next(self):
    self.count += 1
    if self.count > self.max:
      raise StopIteration()
    else:
      return self.count
    
class CounterIterator(Iterator):
  def __init__(self):
    super().__init__(Counter(10))

counter_iterator = CounterIterator()

for count in counter_iterator:
  print(count)
 
    
from pypattyrn.behavioral.mediator import Mediator

class Dog(object):
  sound = ''
  
  def set_sount(self, sound):
    self.sound = sound

class Cat(object):
  sound = ''
  
  def set_sound(self, sound):
    self.sound = sound
    
 dog = Dog()
 cat = Cat()
 
 mediator = Mediator()
 
 mediator.connect('set_dog_sound', dog.set_sound)
 medaitor.conenct('set_cat_sound', cat.set_sound)
 
 mediator.connect('set_sound', dog.set_sound)
 mediator.connect('set_sound', cat.set_sound)
 
 mediator.signal('set_sound', 'foo')

assert 'foo' == dog.sound
assert 'foo' == cat.sound

mediator.signal('set_dog_sound', 'woof')
mediator.signal('set_cat_sound', 'meow')

assert 'woof' == dog.sound
assert 'meow' == cat.sound

mediator.disconnect('set_sound', dog.set_sound)

assert 'woof' == dog.sound
assert 'bar' == cat.sound

### Memento Pattern


```

```sh
pip install pypattyrn
git clone https://github.com/tylerlaberge/PyPattyrn.git
cd PyPattyrn
python setup.py install
```

```
```


