#events #dads-birthday #journal #calander #Python
Import datetime, save to python.py file;
```python
import datetime
t = datetime.datetime.now()
print(t)
```

**Expected Result:**
```shell
2025-12-26 17:26:28.234543
```

Using ptyz:
```python
from datetime import datetime
import pytz

tz = pytz.timezone('Asia/Kolkata')
ct = datetime.now(tz)
print(ct)
```
