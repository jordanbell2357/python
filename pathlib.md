# pathlib

```python
from pathlib import Path
import csv

fieldnames = ['emp_name', 'dept', 'birth_month']

csv_file_path  = Path().cwd() / 'employee_file.csv'

csv_file_path.stem
# 'employee_file'

csv_file_path.suffix
# '.csv

csv_file_path.

csv_file_path.exists()
# False

csv_file_path.is_file()
# False

with open(csv_file_path, mode='w') as csv_file:
    csv_writer = csv.DictWriter(csv_file, fieldnames=fieldnames)
    csv_writer.writeheader()
    csv_writer.writerow({'emp_name': 'John Smith', 'dept': 'Accounting', 'birth_month': 'November'})
    csv_writer.writerow({'emp_name': 'Erica Meyers', 'dept': 'IT', 'birth_month': 'March'})

csv_file_path.exists()
# True

csv_file_path.is_file()
# True

list(Path().cwd().glob('*.csv'))
# [PosixPath('/home/ubuntu/rp/working-with-files-in-python/employee_file.csv')]

with open(csv_file_path, mode='r') as csv_file:
    csv_reader = csv.DictReader(csv_file)
    csv_contents = list(csv_reader)

csv_contents[0]['emp_name']
# 'John Smith'
```
