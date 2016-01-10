The JS models are very simple to use
JS already has a ModelBase which takes care of all logic

* To create a model:
```
from mongoengine import Document
from JumpScale.data.models.Models import ModelBase

class TestDemo(ModelBase, Document):
    name = StringField(default='master')
```

* To create a namespace, just make sure you inherit from NameSpaceLoader
This can be done by:
```
from JumpScale.data.models.BaseModelFactory import NameSpaceLoader


class MyNameSpace(NameSpaceLoader):
    def __init__(self):
        self.__jslocation__ = "j.data.models.mynamespace"
        super(MyNameSpace, self).__init__(Models)  # Where models are your own defined models
```

* To create generic DemoData:
```
from JumpScale.data.models.DemoData import Populate
Populate.create(outputpath)
```

* To load user-defined data into your db:
```
Populate.load(path=path_to_your_json_objects)
```
