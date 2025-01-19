# csv

```bash
curl -O https://datasets.imdbws.com/name.basics.tsv.gz

gzip -d name.basics.tsv.gz
```

```python
# cut.py

import csv

INPUT_FILE_PATH = 'name.basics.tsv'
OUTPUT_FILE_PATH = 'name.fields.tsv'
FIELDS = [1]

with open(INPUT_FILE_PATH, 'r') as input_file:
    csv_reader = csv.reader(input_file, delimiter='\t')
    with open(OUTPUT_FILE_PATH, 'w') as output_file:
        csv_writer = csv.writer(output_file, delimiter='\t', quotechar='"', quoting=csv.QUOTE_MINIMAL)
        for row in csv_reader:
            output_row = []
            for field in FIELDS:
                output_row.append(row[field])
            csv_writer.writerow(output_row)
```

Cut name field and select all but header

```bash
cut -f 2 name.basics.tsv | tail -n +2 > names.txt # 
```

Then remove header and sort names:

```bash
sort names.txt > names_sorted.txt
```

does the same thing as

```python
import csv

NAME_FILE_PATH = 'names.txt'
SORTED_NAME_FILE_PATH = 'sorted_names.txt'

with open(NAME_FILE_PATH, 'r') as f:
    name_list_newlines = f.readlines()
    name_list = [n.removesuffix('\n') for n in name_list_newlines]
    sorted_name_list = sorted(name_list)
    sorted_name_list_newlines = [n + '\n' for n in sorted_name_list]
    with open(SORTED_NAME_FILE_PATH, 'w') as sorted_file:
        sorted_file.writelines(sorted_name_list_newlines)
```
