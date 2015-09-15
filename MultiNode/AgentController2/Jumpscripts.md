## Jumpscripts interface

A jumpscript must define one method `action` that takes data. Data can be any json serializable object.
The action can return a json serializable object as well

Let's assume we have this jumpscript wich increments any given number by 1

```python
form JumpScript import j


def action(data):
    # do stuff with the data
    j.logger.log('Received data is: %s' % data)

    result = data + 1
    return result
```

Then place this file under in 

```bash
/opt/jumpscale7/apps/agentcontroller2/jumpscripts/test/incrementer.py
```

(create the `test` folder if needed)

> `test` is the domain name in that case

> Also note that after placing the folder under `agentcontroller2/jumpscripts` it can take up to a minute until the
script is distributed to all agents as descriped per [Scripts Distribution](ScriptsDistribution.md)


Now to execute your script do the following in a `js` shell. Make sure you have latest  agentcontroller2_client installed:


```python
client =  j.clients.ac.getByInstance('main')

job = client.execute_jumpscript(1, 1, 'test', 'incrementer', data=10)

result = job.get_result()

#`result` should be like this:
{u'args': {u'domain': u'test',
  u'loglevels': [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 20, 21, 22, 23, 30],
  u'name': u'test',
  u'stats_interval': 60},
 u'cmd': u'jumpscript',
 u'data': u'12',
 u'gid': 1,
 u'id': u'ac556dca-ebf6-4494-90f9-4fea16eb9087',
 u'level': 20,
 u'nid': 1,
 u'starttime': 1442320129165,
 u'state': u'SUCCESS',
 u'time': 1058}
```

Note that, `result['data']` is the json (`level 20`) serialized return of the jumpscript, to get it's value you can do:

```python
data = json.loads(result['data'])
```