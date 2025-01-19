# csv

```
cut -f 2 name.basics.tsv > col2.txt

tail -n +2 col2.txt | sort > col2_sorted.txt
```

```
import csv

INPUT_FILE_PATH = 'name.basics.tsv'
OUTPUT_FILE_PATH = 'names.txt'

with open(INPUT_FILE_PATH, 'r') as csv_file:
    csv_reader = csv.reader(csv_file, delimiter='\t')
    with open(OUTPUT_FILE_PATH, 'w') as output_file:
        try:
            current_row = next(csv_reader)  # Get the first row
            while True:
                next_row = next(csv_reader)  # Peek at the next row, if it exists
                output_file.write(current_row[1] + '\n')
                current_row = next_row  # Move to the next row
        except StopIteration:
            output_file.write(current_row[1])

with open(OUTPUT_FILE_PATH, 'r') as f:
    name_list = f.readlines()
    print(len(name_list))
```

14103092 and if we also do `output_file.write(current_row[1] + '\n')` in the `except` block, we also get 14103092.
