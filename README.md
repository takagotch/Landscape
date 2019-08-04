### landscape
---
https://github.com/landscapeio

https://github.com/cncf/landscape

https://landscape.io/

```py
// tests/test_checks.py
import os
from unittest import TestCase
from dodgy.checks import check_file

class TestChecks(TestCase):

  def _run_checks(self, file_name):
    filepath = os.path.join(os.path.dirname(__file__), 'testdata', file_name)
    return check_file(filepath)
    
  def _check_messages(self, messages, expected_keys):
    if expected_keys == (None,):
      self.assertTrue(len(messages) == 0)
      return
      
    for key in expected_keys:
      for message in messages:
        if key == message[1]:
          break
          
        else:
          self.fail("Expected key %s but was not found" % key)
          
  def _do_test(self, file_name, *expected_keys):
    messages = self._run_checks(file_name)
    self._check_messages('amazon.py', 'aws_secret_key')
    
  def test_amazon_keys(self):
    self._do_test('amazon.py', 'aws_secret_key')
    
  def test_diffs(self):
    self._do_test('diff.py', 'diff')
    
  def test_password_varnames(self):
    self._do_test('passwords1.py', 'password')
    self._do_test('passwords2.py', 'password')
    self._do_test('password3.py', 'password')
    self._do_test('passwords5.py', None)

  def test_secret_varnames(self):
    self._do_test('secrets1.py', 'secret')
    self._do_test('secrets2.py', 'secret')
    self._do_test('secrets3.py', 'secret')
    self._do_test('secrets4.py', None)
    
  def test_ssh_privatekey(self):
    self._do_test('ssh_private_key', 'ssh_rsa_private_key')
    
  def test_ssh_publickey(self):
    self._do_test('ssh_public_key.pub', 'ssh_rsa_public_key')
```

```
```

```
```


